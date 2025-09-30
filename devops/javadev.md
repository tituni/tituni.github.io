## Setting up Java development environment

These instructions are tested using Visual Studio Code in Windows.

1.	Install dev containers plug-in for VS

    ![devcontainers](./img/devcontainers_vscode.png)

2.	Create a new dev container in VSCode, first open devcontainer menu (see down left corner):

     ![devcontainers2](./img/devcontainers_vscode2.png)

     Select create new container, select "Java" 

     ![devcontainers3](./img/new_dev_container.png)

     ![devcontainers4](./img/java_dev_container.png)

3. Install Gradle [see](https://docs.gradle.org/current/userguide/installation.html)

    ```cmd
    sdk install gradle
    ```

4. Create a Java-application project template with gradle [see](https://docs.gradle.org/current/userguide/part1_gradle_init.html):

    ```cmd
    $ gradle init --type java-application  --dsl kotlin
    ```

    This is what you get:
     ![gradle templates](./img/templatefiles.png)




