---
title: ThreeJs开发文档
categories: ThreeJs学习
date: 2024-09-02 12:01:51
tags:
    - ThreeJs
comments: false
top_img: false
---

## 初始化模版

### 拉取项目

Starter CODE: [https://github.com/codebucks27/Apple-iphone-3d-landing-page-starter-Code](https://www.youtube.com/redirect?event=comments&redir_token=QUFFLUhqbktHNk1meUJBc0Voc3Bid2FNWjRzTVltVUlFUXxBQ3Jtc0tuT1NjbUwzZ1lnTFZ0MHdmeFYyQTh3V0MyaEJJaDBhNEY5ZUlpcFctN0RLYW9vdUd6OWN5VnhOSVJZVkdqYWF5dzJwcUVuM1J4VTNicVlRcm5fUjlmbW5uOWt5bF9rZFVVa195c1BLMm1fWlMzenlzaw&q=https%3A%2F%2Fgithub.com%2Fcodebucks27%2FApple-iphone-3d-landing-page-starter-Code) 

Final CODE: [https://github.com/codebucks27/3D-Landing-page-for-Apple-iPhone](https://www.youtube.com/redirect?event=comments&redir_token=QUFFLUhqbGo0R2JfUDB5aER2NkM3MnNpU1k4dE9ZYmVfZ3xBQ3Jtc0tsZV80ZURhTUhfWGVDQ28zSVhGdnpoY1BlclVTRXNuMHJNMkt5U0w4Y1NKbUtCQ2YycGJjSmZJY2pGekc3eHFCMWRBdXZLX1dQMjl6bEZSZWdfU25hQmE2Q0cwQm1RblR2WHNNMk5nN1lyaU91c0dqZw&q=https%3A%2F%2Fgithub.com%2Fcodebucks27%2F3D-Landing-page-for-Apple-iPhone) 

## 编写

### 编写全局文件

1）编写`GlobalStyle.js`定义全局样式，并在`App.js`引入

### 编写Quete.js

1）新建`sections/Quote.js`文件，并且安装插件`ES7+ React/Redux/React-Native/JS snippets`  即可在`js`文件中使用 `rafce`生成

```js
import React from 'react'
const Quote = () => {
  return (
    <div>Quote</div>
  )
}
export default Quote
```

并且在`APP.js`引入

2）编写Quote.js，添加文字动画

```js
import React from 'react'
import styled, { keyframes } from "styled-components";

// 定义一个Section组件，使用styled-components库
const Section = styled.section`
  width: 100vw;
  height: 100vh;
  position: relative;

  display: flex;
  justify-content: center;
  align-items: center;
`;

const TextContainer = styled.div`
  width: 100%;
  height: 100%;

  display: flex;
  // 设置主轴方向为从上到下。
  flex-direction: column;
  // 在主轴上居中内容。
  justify-content: center;
  // 在交叉轴上居中内容。
  align-items: center;

  background-color: var(--dark);
  color: var(--white);
`;

const moveUp = keyframes`
100%{
    transform: translateY(0);
}
`;

const Text = styled.p`
  width: 50%;
  font-size: var(--fontlg);
  position: relative;
  height: var(--fontmd);
  overflow: hidden;

  span {
    position: absolute;
    transform: translateY(3rem);
    animation-name: ${moveUp};
    animation-duration: 2.5s;
    animation-timing-function: ease;
    // 在动画完成后，保持动画的最终状态
    animation-fill-mode: forwards;
    animation-delay: ${(props) => props.delay};
    font-family: var(--fontL);

    // 通过背景渐变设置背景图片
    background-image: linear-gradient(-45deg, var(--gradient));
    // 通过背景剪切设置背景图片
    background-clip: text;
    // 针对webkit浏览器设置背景剪切
    -webkit-background-clip: text;
    // 针对webkit浏览器设置文本填充颜色
    -webkit-text-fill-color: transparent;
  }

  // 作者部分
  .author {
    width: 100%;
    text-align: end;
    background-image: linear-gradient(-180deg, var(--gradient));
    font-family: var(--fontR);
  }

  @media screen and (max-width: 70em) {
    width: 70%;
  }

  @media screen and (max-width: 48em) {
    font-size: var(--fontmd);
    height: var(--fontsm);
  }
  @media screen and (max-width: 40em) {
    width: 90%;
  }
  @media screen and (max-width: 30em) {
    font-size: var(--fontxs);
  }
`;


const Quote = () => {
  return (
    <Section>
       <TextContainer>
          <Text delay="0s">
            {" "}
              <span>&#8220; You can't connect the dots looking forward;</span>
            {" "}
          </Text>
          <Text delay="0.4s">
            {" "}
              <span>
                &nbsp;&nbsp;&nbsp;you can only connect them looking backward.
              </span>
            {" "}
          </Text>
          <Text delay="0.8s">
            {" "}
              <span>&nbsp;&nbsp;&nbsp;so you have to trust that the dots</span>
            {" "}
          </Text>
          <Text delay="1.2s">
            {" "}
              <span>
                &nbsp;&nbsp;&nbsp;will somehow connect in your future. &#8221;
              </span>
            {" "}
          </Text>
          <Text delay="1.6s">
            {" "}
              <span className="author">&#x23AF; Steve Jobs</span>
            {" "}
          </Text>
       </TextContainer>
    </Section>
  )
}

export default Quote
```



### 编写HeroSection.js

1）新建section/HeroSection.js文件，输入`rafce`生成

```js
import React from 'react'

const HeroSection = () => {
  return (
    <div>HeroSection</div>
  )
}

export default HeroSection
```

2）在`App.js`引入HeroSection组件

```js
import HeroSection from './sections/HeroSection';

function App() {
  return (
    <>
      <HeroSection />
    </>
  );
}

export default App;
```

3）编写HeroSection.js

```js
import React from 'react'
import styled from "styled-components";
import backgroundVideo from "../assets/video/Ink - 21536.mp4";

const Section = styled.section`
  width: 100vw;
  height: 100vh;
  position: relative;

  display: flex;
  justify-content: flex-end;
  align-items: center;

  background-color: var(--dark);
  overflow: hidden;
`;

const Title = styled.h1`
  position: absolute;
  top: 2rem;
  left: 2rem;

  font-size: var(--fontlg);
  font-family: var(--fontL);
  color: var(--greyLight);

  @media screen and (max-width: 48em) {
    font-size: var(--fontmd);
    left: 1rem;
  }

  @media screen and (max-width: 30em) {
    width: 70%;
    color: var(--white);
  }
`;
const TextContainer = styled.div`
  width: 100%;
  height: 100vh;

  display: flex;
  justify-content: space-between;
  align-items: center;

  background-image: linear-gradient(45deg, var(--gradient));
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  z-index: 1;

  span {
    font-size: var(--fontxxxl);
    text-transform: uppercase;
    font-weight: 600;
    padding: 2rem;

    @media screen and (max-width: 64em) {
      font-size: var(--fontxxl);
      padding: 0;
    }
    @media screen and (max-width: 48em) {
      font-size: var(--fontxl);
    }
  }

  @media screen and (max-width: 48em) {
    flex-direction: column;
    background-image: linear-gradient(90deg, var(--gradient));
    align-items: flex-start;
    filter: brightness(1.1);

    & > *:last-child {
      align-self: flex-end;
    }

    height: 80vh;
    padding: 0 1rem;
  }
`;

const VideoContainer = styled.div`
  width: 100vw;
  min-height: 100vh;

  position: absolute;
  top: 0;
  left: 0;
  z-index: 0;

  video {
    width: 100%;
    height: 100vh;
    object-fit: cover;
    object-position: bottom;
  }
`;


const HeroSection = () => {
  return (
    <Section>
      <VideoContainer>
        <video src={backgroundVideo} type="video/mp4" autoPlay muted loop />
      </VideoContainer>
      <Title>iPhone 14 Pro Max</Title>
      <TextContainer>
        <span>So.Cold.</span>
        <span>So.Bold.</span>
      </TextContainer>
    </Section>
  )
}

export default HeroSection
```

### 模型格式转化

1）gltf格式的3D模型需要格式转化

使用github项目：https://github.com/pmndrs/gltfjsx

使用

```sh
npx gltfjsx model.gltf --transform
// 指定model.gltf，生成model.jsx文件
```

### 编写HeroSection.js

```js
import React from 'react'
import styled from "styled-components";
import { Canvas } from "@react-three/fiber";
import { OrbitControls } from "@react-three/drei";
import { Model } from "../assets/3D-Model/Scene"
import { Environment } from "@react-three/drei";


const Container = styled.div`
  width: 100vw;
  height: 100vh;
  position: fixed;
  top: 0;
  z-index: 1;
  background-color: transparent;
  transition: all 0.3s ease;
`;

/**
 * ambientLight是一个环境光，可以照亮整个场景
 * directionalLight是一个平行光，可以照亮整个场景
 * position={[0, 0, 5]} 表示光源的位置在 (0, 0, 5) 
 * 改变光源的位置和方向可以改变场景的光照效果
 * mesh是一个容器，可以包含多个子元素
 * boxGeometry是一个立方体
 * OrbitControls是一个控制器，可以控制相机的位置和方向
 * meshStandardMaterial是一个材质，可以控制物体的颜色和光照效果
 * @returns 
 */
const PhoneModel = () => {
  return (
    <Container id="phone-model">
        <Canvas>
            <ambientLight intensity={1.25} />
            <directionalLight intensity={0.4} />
            <Model />
            <Environment preset="night" />
            {/* <mesh>
                <boxGeometry />
                <meshStandardMaterial color="red" />
            </mesh> */}
            <OrbitControls />
      </Canvas>
    </Container>
  )
}

export default PhoneModel
```

2）环境光可以参考：

```js
<Environment preset="night" />
```

https://docs.pmnd.rs/

