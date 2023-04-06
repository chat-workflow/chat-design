# 软件需求设计

## 创建系统设计

我们来设计一个流程，名为： demand，其用于软件需求设计。

我们会把设计分为四个部分，你准备好请回复：我准备好了。

### 第一部分

当我使用 "project:{}" 发送你项目基本依赖时，你需要：

1. 记录下这个项目基本情况、使用的技术栈、第三方库信息等。
2. 后续方案都基于这个项目场景，尽可能覆盖异常场景。

以上内容明白吗？明白就只返回：OK。



### 第二部分

当我用 "design:{}" 发给你需求时，示例："design:前端微服务"，你需要： 

1. 使用思维导图模式描述需求的功能模块、相应的 API、以及发散一些非功能性需求。
2. 分析所有潜在的对应场景，分析用户使用场景。 并只返回 Mermaid 格式代码。

以上内容明白吗？明白就只返回：OK。



### 第三部分

当我用 "module: {}" 发给你需求时，示例："module: 子应用动态接入模块"，你需要： 

1. 首先100字概括一下模块需要完成什么功能，

2. 接着，你还需要使用 PlantUML 进行以下工作，并且要考虑各种可能出现的异常场景：

   1. 绘制详细的 Activity Diagram，并只返回 PlantUML 的  Activity Diagram 代码，返回格式如：

      ```
      @startuml
      :Hello world;
      :This is defined on
      several **lines**;
      @enduml
      ```

      

   2. 绘制详细的 Use Case Diagram，并只返回 PlantUML 的  Sequence Diagram 代码，返回格式如：

      ```
      @startuml
      (First usecase)
      (Another usecase) as (UC2)
      usecase UC3
      usecase (Last\nusecase) as UC4
      @enduml
      ```

      

   3. 绘制详细的 Component Diagram，并只返回 PlantUML 的  Component Diagram 代码，返回格式如：

      ```
      @startuml
      [First component]
      [Another component] as Comp2
      component Comp3
      @enduml
      ```

      

   4. 绘制详细的 Sequence Diagram，并只返回 PlantUML 的  Sequence Diagram 代码，返回格式如：

      ```
      @startuml
      Alice -> Bob: Authentication Request
      Bob --> Alice: Authentication Response
      
      Alice -> Bob: Another authentication Request
      Alice <-- Bob: Another authentication Response
      @enduml
      ```

   5. 绘制详细的 State Diagram，并只返回 PlantUML 的  State Diagram 代码，返回格式如：

      ```
      @startuml
      Class01 <|-- Class02
      Class03 *-- Class04
      Class05 o-- Class06
      Class07 .. Class08
      Class09 -- Class10
      @enduml
      ```

   6. 绘制详细的 Class Diagram，并只返回 PlantUML 的  Class Diagram 代码，返回格式如：

      ```
      @startuml
      Class01 <|-- Class02
      Class03 *-- Class04
      Class05 o-- Class06
      Class07 .. Class08
      Class09 -- Class10
      @enduml
      ```


以上内容明白吗？明白就只返回：OK。





### 第四部分

我会用 "system({}):{}" 的形式发给你设计需求，示例："system("API"): 博客系统"，表示上面格式中的 API 部分。要求如下： 

1. 你需要考虑围绕这一类型系统的所有场景。 

2. 使用如下的 DSL 格式来描述系统：

```
   System("BlogSystem") {
     Entities {
       Blog { title: string, ..., comments: [Comment]? },
       Comment { ...}
     }
     Operation {
       Ops("CreateBlog", {
        in: { title: string, description: string },
        out: { id: number }
        pre: title is unique and (title.length > 5 && title.length < 120)
        post: id is not null
       })
     }
     API {
       Route(path: String, method: HttpMethod operation: Operation)
     }
   }
```

以上内容明白吗？明白就只返回：OK。



以上是全部的流程内容，接下来的部分是我的提问。

## 输入：前置数据

project: 以下是项目的基本依赖，后续的对话都是基于这个项目展开，用项目A代替。

```json
{
    "version": "1.0.0",
    "dependencies": {
        "@babel/polyfill": "^7.12.1",
        "@vue/composition-api": "^1.4.3",
        "@vueuse/core": "^9.1.0",
        "axios": "0.17.1",
        "co": "4.6.0",
        "compression-webpack-plugin": "^10.0.0",
        "core-js": "^3.22.7",
        "css-vars-ponyfill": "^2.2.1",
        "dayjs": "^1.10.4",
        "dompurify": "^2.4.0",
        "echarts": "5.2.2",
        "js-md5": "^0.7.3",
        "less": "^4.1.2",
        "lodash-es": "^4.17.11",
        "regenerator-runtime": "^0.13.9",
        "url": "^0.11.0",
        "vue": "2.6.12",
        "vue-class-component": "^7.2.6",
        "vue-property-decorator": "^8.4.2",
        "vue-router": "^3.5.0",
        "vuex": "^3.0.1",
        "vuex-class": "^0.3.2"
    },
    "devDependencies": {
        "@antv/g6": "^4.3.11",
        "@babel/core": "^7.18.2",
        "@babel/eslint-parser": "^7.17.0",
        "@babel/helper-module-imports": "^7.0.0",
        "@babel/parser": "^7.18.4",
        "@babel/plugin-proposal-class-properties": "^7.17.12",
        "@babel/plugin-proposal-nullish-coalescing-operator": "^7.18.6",
        "@babel/plugin-proposal-optional-chaining": "^7.7.4",
        "@babel/plugin-syntax-jsx": "^7.17.12",
        "@babel/plugin-transform-modules-commonjs": "^7.18.2",
        "@babel/plugin-transform-runtime": "^7.18.2",
        "@babel/plugin-transform-strict-mode": "^7.16.7",
        "@babel/preset-env": "^7.18.2",
        "@babel/preset-es2015": "^7.0.0-beta.53",
        "@idux-vue2/cdk": "1.4.0",
        "@idux-vue2/components": "1.4.0",
        "@idux-vue2/pro": "1.4.0",
        "@vue/cli": "^5.0.4",
        "@vue/cli-service": "^5.0.4",
        "@vue/compiler-dom": "^3.2.45",
        "@vue/compiler-sfc": "^3.2.39",
        "@vue/runtime-inject-plugin": "^1.0.7",
        "autoprefixer": "^10.4.7",
        "babel-helper-vue-jsx-merge-props": "^2.0.3",
        "esbuild": "^0.17.10",
        "eslint": "^7.0.0",
        "eslint-plugin-cypress": "^2.12.1",
        "eslint-plugin-lodash": "^7.4.0",
        "eslint-plugin-vue": "^8.4.1",
        "eslint-webpack-plugin": "^3.1.1",
        "external-remotes-plugin": "^1.0.0",
        "less-loader": "^10.2.0",
        "mini-css-extract-plugin": "^2.6.0",
        "stylelint": "^11.0.0",
        "typescript": "^4.5.5",
        "unplugin-auto-import": "^0.11.4",
        "unplugin-vue2-script-setup": "^0.11.3",
        "vue-eslint-parser": "^8.3.0",
        "vue-hot-reload-api": "2.1.0",
        "vue-loader": "^17.0.0",
        "vue-style-loader": "^4.1.3",
        "vue-template-compiler": "2.6.12",
        "webpack": "5.72.1",
        "webpack-manifest-plugin": "^5.0.0",
        "babel-plugin-istanbul": "^6.1.1"
    }
}
```

分析完成就返回 100 字概括项目情况。



## 输入：技术选型

实现前端微服务的能力目前有哪些主流的技术，他们在开发效率、部署难度、维护成本、可维护性、架构复杂度、可扩展性上的优缺点，并用表格返回。



## 输入：分析技术需求

> *这里可以先生成主要的需求分析*

design: 使用module federation 实现前端微服务，并且要做到独立升级、独立部署、子应用功能自治理。

首先用200字概括一下技术可行性。接着，现在你要进行以下工作：

1. 分析该需求的功能模块。并按照下边格式返回：

   ```
   1. 模块1
       - 功能1
       - 功能2
   2. 模块2
       - 功能1
       - 功能2
   ```

2. 根据上文的功能列表，输出相应的 API。只返回 API 部分，并使用表格绘制。

3. 发散一些非功能性需求。并按照下边格式返回：

   ```
   安全性
       - 注意点1
       - 注意点2
   可扩展性
       - ...
   可靠性
       - ...
   可维护性
       - ...
   性能
       - ...
   ```

   



## 输入：使用 mermaid 输出设计图

> 根据功能列表划分模块，重复执行该环节直至所有的内容都生成。

module: 动态加载子应用模块。

首先100字概括一下模块需要完成什么功能；

接着，你还需要使用 Mermaid 进行以下工作，并且要考虑各种可能出现的异常场景：

1. 绘制详细的 Flowchart Diagram，并只返回 Mermaid 的  Flowchart Diagram 代码，返回格式如：

   ```mermaid
   graph
       A(开始) --> C(待补充) --> B(结束)
   ```

   

2. 绘制详细的 Sequence Diagram，并只返回 Mermaid 的  Sequence Diagram 代码，返回格式如：

   ```mermaid
    sequenceDiagram
        participant 小明
        participant 小红
        小明->>小红: 早 小红
        小红->>小明: 早上好
   ```

3. 绘制详细的 State Diagram，并只返回 Mermaid 的  State Diagram 代码，返回格式如：

   ```mermaid
    stateDiagram
        [*] --> 启动
        启动 --> [*]
        启动 --> 移动
        移动 --> [*]
   ```

4. 绘制详细的 Class Diagram，并只返回 Mermaid 的  Class Diagram 代码，返回格式如：

   ```mermaid
   classDiagram
       Animal <|-- Duck
       Animal <|-- Fish
       Animal <|-- Zebra
       Animal : +int age
       Animal : +String gender
       Animal: +isMammal()
       Animal: +mate()
   ```





## 输入：使用 PlantUML 输出设计图

> 根据功能列表划分模块，重复执行该环节直至所有的内容都生成。

module: 动态加载子应用模块。

首先100字概括一下模块需要完成什么功能，

接着，你还需要使用 PlantUML 进行以下工作，并且要考虑各种可能出现的异常场景：

1. 绘制详细的 Activity Diagram，并只返回 PlantUML 的  Activity Diagram 代码，返回格式如：

   ```
   @startuml
   :Hello world;
   :This is defined on
   several **lines**;
   @enduml
   ```

   

2. 绘制详细的 Use Case Diagram，并只返回 PlantUML 的  Sequence Diagram 代码，返回格式如：

   ```
   @startuml
   (First usecase)
   (Another usecase) as (UC2)
   usecase UC3
   usecase (Last\nusecase) as UC4
   @enduml
   ```

   

3. 绘制详细的 Component Diagram，并只返回 PlantUML 的  Component Diagram 代码，返回格式如：

   ```
   @startuml
   [First component]
   [Another component] as Comp2
   component Comp3
   @enduml
   ```

   

4. 绘制详细的 Sequence Diagram，并只返回 PlantUML 的  Sequence Diagram 代码，返回格式如：

   ```
   @startuml
   Alice -> Bob: Authentication Request
   Bob --> Alice: Authentication Response
   
   Alice -> Bob: Another authentication Request
   Alice <-- Bob: Another authentication Response
   @enduml
   ```

5. 绘制详细的 State Diagram，并只返回 PlantUML 的  State Diagram 代码，返回格式如：

   ```
   @startuml
   Class01 <|-- Class02
   Class03 *-- Class04
   Class05 o-- Class06
   Class07 .. Class08
   Class09 -- Class10
   @enduml
   ```

6. 绘制详细的 Class Diagram，并只返回 PlantUML 的  Class Diagram 代码，返回格式如：

   ```
   @startuml
   Class01 <|-- Class02
   Class03 *-- Class04
   Class05 o-- Class06
   Class07 .. Class08
   Class09 -- Class10
   @enduml
   ```






