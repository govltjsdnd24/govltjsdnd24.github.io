---
categories: [ Development, React ]
tags: [ three.js ] 
---

The front-end part of my current project is progressing at a fast speed, and since I am constantly being hurled at novel things to learn every step I make, I had to make a new post almost right after I wrote one. This article is continued from the one before so I advice you take a look at that first. 

## Keyboard Input

We imported the model and imeplemented animation on it. Now it's time to make it move according to keyboard inputs. 

First and foremost, we import the required libraries.

```javascript
import { KeyboardControls} from '@react-three/drei';
import Controller from 'ecctrl'
```
The <i>KeyboardControls</i> library is in charge of connecting the customized keyboard layout to the useKeyboard hook. (Remember that hooks all come in the form of use***). The Controller library is a useful library that uses the keyboard mapping provided to the movement of the character, including jump and sprint. The latter is especially recommended to use because it just facilitates the entire process by a LOT.

```js
const keyboardMap = [
    { name: 'forward', keys: ['ArrowUp', 'KeyW'] },
    { name: 'backward', keys: ['ArrowDown', 'KeyS'] },
    { name: 'leftward', keys: ['ArrowLeft', 'KeyA'] },
    { name: 'rightward', keys: ['ArrowRight', 'KeyD'] },
    { name: 'run', keys: ['Space'] },
];

...
<KeyboardControls map={keyboardMap} >
    <Controller maxVelLimit={5}>
    <RigidBody colliders={false} gravityScale={4}>
        <OscillatingMan currentAction={currentAction} /> 
    </RigidBody>
    </Controller>
</KeyboardControls>


```

The next part is keyboard mapping and application. We map the keyboard so that it takes in both WASD and the arrows. Let's also take in the space to trigger running. Then, we move over to the rendering class. Simply place KeyboardControls by propagating the mapped keyboard layout, and locate the Controller within in it. 

The resulting screen would something like this.

![move](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/0f3478e8-fdf9-4bda-b0c7-e4be83f10549)

## Event Hook

Now that we implemented movement based on keyboard input, let's take a look at how to deal with events in react. The event we want to capitalize on are our configured keyboard inputs, and the first thing we have to do is create a function that receives the key press event.

```JS
  const handleKeyDown = (event) => {
  ...interaction with event
  }
```
Something like this perhaps? Don't forget to make a similar function for handleKeyUp! We always want to know when we let go of keys as well.

The event looks like this:

![keyboard_input](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/aa097d93-7c9c-4dcb-bb9e-bd696a6bedb7)

Let's elaborate the code further by adding details into the function. The event would be key press, and look something like "KeyW". We save the input and let it go through our mapping table.

```JS
  const handleKeyDown = (event) => {
    const key=event.code;
    const keyMapping = keyboardMap.find((entry) => entry.keys.includes(key)).name;
  }
```

This way, we can alter the data into a useful format. Like this!

![keyboard_processed](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/13807ea3-fffb-4d56-970a-911bcea450ea)

Next, we utilize useEffect hook inside our model jsx in order to play animation according to the input, dividing the actions into walk, run, and idle.

```JS
useEffect(() => {
    
    const action = props.action.currentAction;

    if (action === 'forward' || action ==='backward' || action ==='leftward'|| action==='rightward') {
      actions.walking.play();d
    } else if(action ==='run'){
      actions.run.play();
    }
    else {
      actions.idle.play();
    }
  }
);
```

However, here I encountered a problem. 

![moonwalk](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/630f6bbd-a934-49e8-8699-b482da92666d)

Yes, even when standing still, the model is walking. Also, there was a symptom where you switch from one keyboard input to another switfly, the model is stuck in the idle animation and will basically "slide" on the surface. 

I tried a lot of things to make remedy this fault, but didn't know which keyword to type for on Google in the first place. After much attempts, I finally found the problem and fixed it.

We first look at our model's jsx.
```js
useEffect(() => {
    
    const action = props.action.currentAction;
    mixer.stopAllAction();

    if (action === 'forward' || action ==='backward' || action ==='leftward'|| action==='rightward') {
      actions.walking.reset().play();
    } else if(action ==='run'){
      actions.run.reset().play();
    }
    else {
      actions.idle.reset().play();
    }
  }

```

I added a mixer to stop all action after one has been carried out entirely. Also, I supplemented reset() to the code that executes the animation to let it start from the very beginning.

Another thing I did was :

```js

const [pressedKeys, setPressedKeys] = useState(new Set());

const handleKeyDown = (event) => {
        const key = event.code;
        const find=keyboardMap.find((entry) => entry.keys.includes(key))
        if(find!=null){
          const keyMapping = find.name;
          setPressedKeys((prevKeys) => new Set([...prevKeys, keyMapping]));
          setCurrentAction(keyMapping);
        }
      };
      
      const handleKeyUp = (event) => {
        const key = event.code;
        const find=keyboardMap.find((entry) => entry.keys.includes(key))
        if(find!=null){
          const keyMapping = find.name;
          setPressedKeys((prevKeys) => new Set([...prevKeys].filter((k) => k !== keyMapping)));
          if(pressedKeys.size<2)
            setCurrentAction("idle");
        }
      };

```

I created a state in a set form to memorize all currently pressed keyboard inputs. The set will make sure that there are no duplicate values saved, and will allow strings to be added and subtracted dynamically. I made sure that the idle animation will only take place when there are only 0 or 1 inputs stored in the set. This prevented the slidiing phenomenon caused from multiple inputs. Also, I blocked any inputs other than the ones I configured.

Through this process, I was able to implement a full and functional game-like environment.

![success](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/5256d733-9a48-46cd-b122-12cec8f8116a)

## Conclusion 
Finally! I added all the rudimentary parts of a game! Of course, I'm not trying to make a game here, but movement plays a key role in my current project, and being able to succesfully construct the system from ground up in a foreign domain such as three.js is indisputably a worthy accomplishment.

## Reference
[https://threejs.org/docs/#manual/ko/introduction/Loading-3D-models](https://threejs.org/docs/#manual/ko/introduction/Loading-3D-models)





