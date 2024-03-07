---
categories: [ Development, React]
tags: [ three.js ] 
---

Last post, we covered the topic of models and simple animations. However, we can't really call this an animation, but rather just a plain, repetitive movement--such that would befit the UI elements. In order to deliver a more immersive and life-like user experience, applying animation to model is obligatory. I will also cover the topic of colliders, since an animation would be mererly a janky flailing of limbs if not carried out on a proper surface.

## Application of Animation on Models

So, last time I talked about the ways of importing different types of model files. This post, I am going to be exclusively utilizing the glb file extension, because of its applicability and ease of use; it is difficult to appertain animation on an fbx file, and gltf files are hard to keep track of because of their disseminated nature.

First off, we fetch the model and animation. A great website for this is Mixamo. Mixamo allows its users a library of characters and animations to use. Furthermore, users can bring their own model (in fbx file format) and attach skeletal points on it; this will be especially useful because the default characters available on the website is plain HORRIBLE. 

![alt text](image.png)

Their archive of animations is, on the other hand, very useful, and I strongly advise you use it. I tried uploading my fbx model primarily, but discovered later on that it was a faulty one, so had to retrogress to choosing the default model. Choose to download the animation <u>along with the model</u>. I found it much easier to do this over just downloading the animation, even risking the trade-off of having a large size project.

![alt text](image-1.png)

After you acquire the model and animation, it's time for you to render it to a glb file. You must first download Blender (don't worry it's free), and import the fbx file into the software. Now you would get a screen that resembles something like this:

![alt text](image-2.png)

Here, you must edit the name of the animation, because you have to be able to refer to it later on in the model's JSX file. For this, click on the dropdown menu on the lower compartment. It should originally say <i>Dope sheet</i>. You must change this to <i>Action Editor</i>
![alt text](image-3.png)

Then, change the name of the animation by clicking on the dropdown box with the animation list. Change it to something much simpler.
![alt text](image-4.png)

Now that you've renamed the animation, export the model to a glb format, and head to your React project. Move your model to anywhere in your public folder--I moved it to a subdirectory called <i>models</i>. Now access the terminal and type in
```bash
npx gltfjsx <model_name>.glb
```
inside the directory with the model. This should create the JSX file for the model. Now you move this to the <i>src</i> folder, like you did last time. Then, it's time for you to add a code block that would catalyze the animation.

```JSX
useEffect(()=>{
    actions.<action_name>.play();
  })
```
Yes. It's that simple. FYI, this would be my full JSX code.

```JSX
import React, { useEffect, useRef } from 'react'
import { useGLTF, useAnimations } from '@react-three/drei'

export function Model(props) {
  const group = useRef()
  const { nodes, materials, animations } = useGLTF('/models/hiphop.glb')
  const { actions } = useAnimations(animations, group)
  useEffect(()=>{
    actions.capoeira.play();
  })
  return (
    <group ref={group} {...props} dispose={null}>
      <group name="Scene">
        ...details of model
      </group>
    </group>
  )
}

export default Model;

useGLTF.preload('/models/hiphop.glb')
```

## Collider
Now, your model will be moving in your own three.js environment. But, as I said before, without a ground to stand on, the movement would feel weird. Let's apply colliders to our models. Move to your App.js.

Frist thing you should do is import the necessary packages and libraries.
```javascript
import { Canvas,useFrame } from '@react-three/fiber';
import { OrbitControls, KeyboardControls} from '@react-three/drei';
import { useSpring, animated, config } from "@react-spring/three";
import { Physics, RigidBody } from '@react-three/rapier'
import Controller from 'ecctrl'
```

Not all the libraries listed here are essential for colliders; I implemented movement with keyboard as well, hence the extra libraries. The library you should be focused on is <i>react-three/rapier</i>, which provides really helpful modules like Physics and RigidBody.

```javascript 
<Physics timeStep="vary">
    <KeyboardControls map={keyboardMap}>
        <Controller maxVelLimit={5}>
            <RigidBody colliders={false} gravityScale={4}>
                <OscillatingMan /> 
            </RigidBody>
        </Controller>
    </KeyboardControls>

    <RigidBody type="fixed">
        <mesh>
            <boxGeometry attach="geometry" args={[10, 1, 10]} />
            <meshBasicMaterial attach="material" color="gray" />
        </mesh>
    </RigidBody>
</Physics>
```
This is the code implementing colliders. Everything should be wrapped in Physics class, because they should all be affected by it. The timeStep vary keyword helps with the elasticity of the environment, which should help in our little,fickle project. Ignore the Keyboard and Controller, and look at the RigidBody class. This class provides the collider necessitated to simulate collision, and other auxiliary factors such as gravity scale. the collider for < OscillatingMan > class is set to false, because it overlaps with the collider that the model has innately.

The <i>RigidBody</i> on the bottom is of "fixed" type. Why is that? That's because it's a plain that the model must stand on, and a ground should be fixed no matter what.

Finally, let's take a look at our result.

![alt text](result.gif)

Perfect.

## Conclusion 
Today, we went over the subject of advanced animation. I'm not still in the level of "Make-your-own-animation", yet, and don't plan to be in a near future. So, for now, this would suffice. I will go over the keyboard input in the next post. Again, thanks for reading my post.

## Reference
[https://threejs.org/docs/#manual/ko/introduction/Loading-3D-models](https://threejs.org/docs/#manual/ko/introduction/Loading-3D-models)
[https://www.mixamo.com/](https://www.mixamo.com/)
[https://www.blender.org/](https://www.blender.org/)




