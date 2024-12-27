---
categories: [ Development, React ]
tags: [ three.js ] 
---


This post, I wish to go over how one could implement three.js--more specifically 3d models--within React. Graphical Engines like Unity and Unreal Engine are excellent tools for game development, but don't quite fit well in the realm of Web. I chose three.js for its popularity and the plethora of data available in the web. Of course, I won't be going too deep in to the subject, not only because of the sake of time, but also my sheer incompetence to do so. Anyways, here it goes.

## Process

``` bash
npm install three
npm install @react-three/drei
npm install @react-three/fiber
```

These are the lines of codes required to download the essentials of Three.js on React. Each library is the core, facilitatory, and implementating library for React, respectively. In case you are curious, fiber is the architecture that React belongs in and it's in charge of the rendering of the said framework; the aforementioned library mitigates the difference between three.js and fiber.

For the model, I got it from sketchfab, a website where you can find various types of models for free or at least a reasonable amount of money. Another reason why I preferred this website was that it provided model files in gltf file, which is in a JSON format comprehsnible by JSX; this is different from binary files such as fbx or glb--which can be converted to JSON file but require additional procedures.

![sketchfab](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/b509b604-7773-40df-87b8-c3be04cd1a1b)

Next, we must convert the gltf file into a jsx file, because it won't be useful to us otherwise. For this step, we first download gltfjsx, then convert the gltf file with the provided command.
```bash
npm install gltfjsx
npx gltfjsx <gltf file>
```
The resulting jsx file would something like this: 

![jsxmodel](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/6c30b975-6888-400c-8af2-c2cc7e5f6a99)

Relocate the folder containing the model to <i>public</i> folder. Then, move the jsx file into the src folder. If you do not do this, three.js is unable to locate the required files and will return errors as such:

![error](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/4f3be362-e7fe-4195-a935-0eaf33c8009d)

Now all you have to do is import the model and display it.

```
import {Model} from './Scene'
...
function App() {
  return (
    <div className="App">
      <Canvas>
      <OrbitControls/>
        <mesh>
          <ambientLight intensity={1}/>
          <directionalLight intensity={1}/>
          <Model/>
          <meshStandardMaterial attach="material" color= {0xa3b18a}/>
        </mesh>
      </Canvas>
    </div>
  );
}
```
Something like this.

> In case you are wondering what the elements indicate, <i>< Canvas ></i> is the plane where the model is displayed. <i> < OrbitControls > </i> allows the user to rotate the model with their mouse. <i> < mesh ></i> is required for the display of the model, and the elements ending with 'Light' are, you guessed it, the light illuminating the objects. Lastly, the meshStandardMaterial is the material wherein the elements will be enveloped in; it's necessary you use this if you want to color the element.

Voila! You were able to import your very first model.

![result_Screen](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/5db33e7e-3f92-46df-9d1a-a17a34e20b63)

## Conclusion 
That was it for the topic of "Three.js in React". It wasn't a very bumpy ride, because there were some guidelines in the internet that I could follow. The only thing holding me back is that most of the data found on the web about Three.js is not conducted within React. I believe additional effort would be required for a seemless tranisition from the original code to a one habitable in React's turf.

## Reference
[https://threejs.org/docs/#manual/ko/introduction/Loading-3D-models](https://threejs.org/docs/#manual/ko/introduction/Loading-3D-models)



