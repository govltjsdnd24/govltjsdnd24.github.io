---
categories: [ Development, React ]
tags: [ three.js ] 
---

Now that we learned about how to implement Three.js in React, let's step ahead to the next phase: Animation. Animation plays a very important role in the presentation of 3d models; without it our 3-dimensional portrayal would be lifeless at best. Thankfully three.js-fiber provides several wonderful tools for us to implement to our project.

## Simple Animation

We start off by importing <i>useFrame</i>, which is a Fiber hook which allows the rendering of Fiber in a loop. Now, hold up, what is a hook? Hook serves the purpose of <u>connecting</u> the chosen element with a specific piece of information, not only allowing delivery of data, but also interaction with it. 
``` JSX
import { useFrame } from '@react-three/fiber'
```

Remember that anything inside the useFrame method is called every frame! This means any animation that we wish to implement should belong within this specific block of code.

Another important aspect of animation is time. Without a way to track time, one cannot accomplish recurring movement, or as we call it, oscillation. This requires a particular keyword <u>clock</u> which records the elapsed time. <i>manMesh</i> is the mesh that the model is covered in, and will be used to manipulate it; every governed object must be covered in this triangular polygon cover. In the code below, the mesh is being rotated in the x direction as time proceeds.
``` JSX
useFrame(({ clock }) => {
  const time = clock.getElapsedTime()
  manMesh.current.rotation.x = a;
})
```
Next, have a look at this code:
```JSX

function OscillatingMan() {
  const manMesh = React.useRef()
  return (
    <mesh ref={manMesh}>
      <Model />
    </mesh>
  )
}
```
manMesh is first being assigned useRef(), which is a hook that is connected to a value not required for rendering; unlinke useState(), it is not updated according to change, and will be used for persistent storage of a value--in this case, the rotational amplitude. A mesh with a reference to manMesh then envelops our model, and forces the model to carry out the ordered movement.

However, what we are yearning for is not a rotation towards one-direction, but rather is, an oscillation. In order to imitate a smooth, perpetual swaying motion, we must use the sin function, which, starting from 0, goes on endlessly to swing between 1 and -1.
```JSX
useFrame(({ clock }) => {
    const time = 3 * clock.getElapsedTime();
    const oscillation = Math.sin(time);
    manMesh.current.rotation.z = 0.5*oscillation; 
  });
```
Some alterations have been made to make the movement happen faster and in shorter interval, but the general idea is identical. I wanted the rotation to take place in z-direction, and have changed it accordingly. After the application of this code block, the result will look something like this:

![oscillate](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/77683bed-d88b-4cf1-9173-61b10d1ce98f)

One can also add a more refined animation upon click event.
```JSX
import { useSpring, animated, config } from "@react-spring/three";
  const [active, setActive] = useState(false);

  const { scale } = useSpring({
    scale: active ? 1.3 : 1,
    config: config.wobbly
  });
  
...

  return (
    <animated.mesh
    scale={scale}
    onClick={() => setActive(!active)}
    ref={myMesh}
  >
      <Model/>
    </animated.mesh>
  );
```
This code will use React-Spring, which is a library that allows fluid transition for UIs and graphical objects, in order to adjust the element's size upon click event--triggered by a <i>active</i> status; it doesn't only adjust the scale, but also adds a wobbly effect in the transition.

![grow-shrink](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/17acd6f9-aa0b-43e9-a3ff-0459035e426b)

Likewise, such animation can be easily implemented to our project. 

In case you would like to import models in fbx extension, which is a much easier format to use because the model is wrapped in a single file, please do as below:

```JSX
import { FBXLoader } from 'three/examples/jsm/loaders/FBXLoader'
...
const fbx = useLoader(FBXLoader, '/models/banker_model_kick.fbx')
...
return (
    <animated.mesh
    scale={scale}
    onClick={() => setActive(!active)}
    ref={myMesh}
  >
      <primitive object={fbx} scale={[0.01, 0.01, 0.01]} />
    </animated.mesh>
  );
```
You must know that the element should be referred to as primitive because it's a pre-existing object. Scale has been applied simply to adjust the size of the model.

The final code, with minor alteration, looks likes this:
```JSX
import React, {useState} from "react";
import { Route, Routes } from "react-router-dom";
import Nav from "./components/Nav";
import Home from "./pages/Home";
import MyPage from "./pages/MyPage";
import Forum from "./pages/Forum";
import Map from "./pages/Map";
import { Canvas,useFrame,useLoader } from '@react-three/fiber';
import { OrbitControls } from '@react-three/drei';
import { useSpring, animated, config } from "@react-spring/three";
import { FBXLoader } from 'three/examples/jsm/loaders/FBXLoader'

import "./styles/common/App.css";

function OscillatingMan() {
  const myMesh = React.useRef();
  const [active, setActive] = useState(false);

  const { scale } = useSpring({
    scale: active ? 1.3 : 1,
    config: config.wobbly
  });

  const fbx = useLoader(FBXLoader, '/models/banker_model_kick.fbx')

  useFrame(({ clock }) => {
    const time_rotate = 2.5* clock.getElapsedTime();
    const time_position = 5* clock.getElapsedTime();
    const oscillation_rotate = Math.sin(time_rotate);
    const oscillation_position = Math.sin(time_position);
    myMesh.current.rotation.z = 0.2*oscillation_rotate; 
    myMesh.current.position.y=0.2*oscillation_position;
  });

  return (
    <animated.mesh
    scale={scale}
    onClick={() => setActive(!active)}
    ref={myMesh}
  >
      <primitive object={fbx} scale={[0.01, 0.01, 0.01]} />
    </animated.mesh>
  );
}

function App() {
  return (
    <div className="App">
      <Nav />
      <Routes>
        <Route exact path="/" element={<Home />} />
        <Route path="/mypage" element={<MyPage />} />
        <Route path="/forum" element={<Forum />} />
        <Route path="/map" element={<Map />} />
      </Routes>
      <Canvas>
      <OrbitControls/>
        <mesh>
          <ambientLight intensity={1}/>
          <directionalLight intensity={1}/>
          <OscillatingMan/>
          <meshStandardMaterial attach="material" color= {0xa3b18a}/>
        </mesh>
      </Canvas>
    </div>
  );
}

export default App;

```

## Conclusion 
That was my attempt at replicating a simple animation. Of course, it's a very elementary level of implementation and thus cannot be said to be completely useful in the actual project, but it's a start. I will eventually go to the next step: using Blender to customize models and their animations.

## Reference
[https://threejs.org/docs/#manual/ko/introduction/Loading-3D-models](https://threejs.org/docs/#manual/ko/introduction/Loading-3D-models)



