# Chapter1. 初识Jersey

\#\# Jersey概述



​	Jersey是一个以Java实现得RESTful Web Service。它可以根据需要，自定义返回media types，例如返回\*text/plain\*，\*application/json\* 等。







\#\# Jersey项目创建 \#\#



​	Jersey官方推荐使用Maven来构建Jersey项目，Jersey支持普通得Java SE来使用，它会内置有Grizzly container 使其成为可以服务端应用。当然，也可是使用Jersey得Maven模板来创建Jersey得Web应用，他能编译成war来方便发布在Servlet容器中\(Servlet2.5 + \)。



​	当然，由于Jersey是可以当作第三方工具包的项目，也可以在已有的项目中引入Jersey的依赖，并配置相关属性来使用Jersey的功能。



​	下面根据官方文档，来介绍两种创建Jersey项目的方式。



- 创建Java SE项目



  \`\`\`shell

  mvn archetype:generate -DarchetypeArtifactId=jersey-quickstart-grizzly2 \

  -DarchetypeGroupId=org.glassfish.jersey.archetypes -DinteractiveMode=false \

  -DgroupId=com.example -DartifactId=simple-service -Dpackage=com.example \

  -DarchetypeVersion=2.25.1

  \`\`\`



  在命令行中，可以使用这段代码来创建Jersey的maven项目，它即会生成一个Jersey官方标准的项目结构，如果使用Eclipse ，IDEA等IDE创建的话，因为默认没有Jersey的模板用例，则必须自己手动添加，流程如下：



  1. 点开Eclipse创建Maven项目的界面，即New Maven project 界面，在这个界面中选中Add Archetype按钮来添加新的模板。



  2. 输入相关信息，即可创建成功，其中Repository Url是选填项，如果需要填写，则可以填下面这个Url



     \`\[https://maven.java.net/content/repositories/snapshots/\]\(https://maven.java.net/content/repositories/snapshots/\) \`



- 创建标准的Java Web项目



  创建Java Web项目其实跟Java SE项目类似，只是maven的命令参数有稍微的改变，即如下：



  \`\`\`shell

  mvn archetype:generate -DarchetypeArtifactId=jersey-quickstart-webapp \

                  -DarchetypeGroupId=org.glassfish.jersey.archetypes -  DinteractiveMode=false \

                  -DgroupId=com.example -DartifactId=simple-service-webapp -Dpackage=com.example \

                  -DarchetypeVersion=2.25.1

  \`\`\`



  在IDE中创建模板的步骤，也如创建Java SE模板相同。



  \#\# Jersey项目结构



  \* Jersey Java SE 项目结构



    ​	基本的结构和普通的maven项目相同，只是Jersey初始化了一些类和主函数，方便运行。具体结构如下图所示:



    !\[Java SE 项目结构\]\(.\Jersey.png\)



    ​	Main函数包含了程序的主入口，它启动后，就会自动运行内置的Container来启动项目,方便别人访问。其中，\` GrizzlyHttpServerFactory.createHttpServer\(URI.create\(BASE\_URI\), rc\); \`这段代码设置了监控的跟URI为\` http://localhost:8080/myapp/ \` ，扫描的包配置为rc，即\` final ResourceConfig rc = new ResourceConfig\(\).packages\("com.em248"\); \` 则我们在\_com.em248\_包或其子包下配置的注解等将会被扫描并注册。



    ​	test包下也包含了一个基本测试的例子，可以方便我们按照这个模板例子来写好测试用例。



  \* Jersey Web 项目结构



    ​	Jersey Web 项目结构和普通的maven webApp 项目结构是一样的，都包含了webapp,web.xml等基本的配置文件，但是，在web.xml文件中，Jersey已经帮我们配置好了其使用的Servlet和扫描注解的包和匹配的URI路径。其中，如果我们使用的是Servlet 3.0的Web 容器，则我们也可以不需要使用web.xml配置文件。大体结构如下图所示：​

    !\[Web项目结构\]\(.\Jersey1.png\)

    ​	其中entity是博主自己手动创建的，在刚开始的时候是没有这个包以及这个包下的内容。\_MyResource.java\_就是给出的基本的使用注解来映射请求的案例。

