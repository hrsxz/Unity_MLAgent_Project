# Unity ML-Agents 强化学习笔记

*使用Unity提供的ML-Agents Toolkit实现一个强化学习游戏。*

## 如何开始这个项目

### 1. 从官网下载安装Unity Hub

[Download Unity Hub](https://unity.com/de/download)

### 2. 从Unity Hub安装Unity 2022.3.18f1

### 3. 根据视频创建一个新的Unity项目

[Unity项目教程](https://www.youtube.com/watch?v=fZy9HRrkNvc&t=807s)

### 4. 添加C# Agent脚本

    Assets/RollerBall.cs

### 5. 改变Behavior Parameters中的behavior type为Heuristic Only 手动测试游戏环境

### 6. 安装ML-Agents

- 分别在ml-agent和ml-agent-envs下面的cmd窗口中执行

    ![Alt text](https://github.com/hrsxz/Unity_MLAgent_Project/blob/master/Image/image.png)

    ![Alt text](image/image.png)

    ```python
    pip install -e .
    ```

- 使用 mlagents-learn --help 检查是否安装成功
- 运行以下命令，启动unity ml agent

    ```python
    mlagents-learn config/rollerball_config.yaml --run-id=firstRun
    ```

### 7. 配置模型的训练参数

1. 基于 C:\AI\unity_projects\ml-agents\config\ppo\rollerball.yaml配置新的模型训练设置保存至C:\AI\unity_projects\ml-agents\config\sample\rollerball.yaml
2. 改正behavior paramters里面behavior name和下图红框中的设置一致。

   ![Alt text](https://github.com/hrsxz/Unity_MLAgent_Project/blob/master/Image/image-2.png)

   ![Alt text](image/image-2.png)

   ![Alt text](https://github.com/hrsxz/Unity_MLAgent_Project/blob/master/Image/image-1.png)

   ![Alt text](image/image-1.png)
3. 使用tensorflow面板监控训练过程

    ```python
   (venv_unity) C:\AI\unity_projects\ml-agents>tensorboard --logdir=results
    Serving TensorBoard on localhost; to expose to the network, use a proxy or pass --bind_all
    TensorBoard 2.15.1 at http://localhost:6006/ (Press CTRL+C to quit)
    ```

    ![Alt text](https://github.com/hrsxz/Unity_MLAgent_Project/blob/master/Image/image-3.png)

    ![Alt text](image/image-3.png)

4. 使用官方推荐的rollerball_config.yaml配置文件进行训练

    ```yaml
    behaviors:
        RollerBall:
            trainer_type: ppo
            hyperparameters:
            batch_size: 10
            buffer_size: 100
            learning_rate: 3.0e-4
            beta: 5.0e-4
            epsilon: 0.2
            lambd: 0.99
            num_epoch: 3
            learning_rate_schedule: linear
            beta_schedule: constant
            epsilon_schedule: linear
            network_settings:
            normalize: false
            hidden_units: 128
            num_layers: 2
            reward_signals:
            extrinsic:
                gamma: 0.99
                strength: 1.0
            max_steps: 500000
            time_horizon: 64
            summary_freq: 10000
    ```

### 8. 使用训练好的模型测试游戏

1. 训练好的模型保存在C:\AI\unity_projects\ml-agents\results里

   ![Alt text](https://github.com/hrsxz/Unity_MLAgent_Project/blob/master/Image/image-4.png)

   ![Alt text](image/image-4.png)
2. .onnx文件是用于在Unity中使用的模型文件

   ![Alt text](https://github.com/hrsxz/Unity_MLAgent_Project/blob/master/Image/image-5.png)

   ![Alt text](image/image-5.png)
3. 将.onnx文件拷贝到当前项目的Assets/Models文件夹下

   ![Alt text](https://github.com/hrsxz/Unity_MLAgent_Project/blob/master/Image/image-6.png)

   ![Alt text](image/image-6.png)
4. 在Unity中设置Behavior Parameters中的behavior type，将Model改为刚刚拷贝的.onnx文件

   ![Alt text](https://github.com/hrsxz/Unity_MLAgent_Project/blob/master/Image/image-7.png)

   ![Alt text](/image/image-7.png)

5. 运行游戏，观察Agent的行为

    ![Alt text](/image/20240128_114054.gif)

## References

[Unity ML-Agents 游戏强化学习笔记](https://techdiylife.github.io/AI-Game/unity/memo-unity-ML-Agents-01.html)
[Unity ML-Agents Toolkit](https://unity-technologies.github.io/ml-agents/Learning-Environment-Create-New/#training-the-environment)
[Unity Github](https://github.com/Unity-Technologies/ml-agents)
[YouTube视频](https://www.youtube.com/watch?v=2N9EoF6pQyE&list=PLX2vGYjWbI0Q-s4_lX0h4i2zbZqlg4OfF&index=1)