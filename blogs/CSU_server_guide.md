## introduction
高性能服务器与常用服务器不同的是，需要任务系统申请GPU，才会排队分配使用
## 步骤
1. 完成代码的编写后，新建一个任务申请脚本 `touch task.sh`，使用 vim 编辑脚本
```shell
#!/bin/sh
#SBATCH -J DCL_JOB 
#SBATCH -o dcl_02.log
#SBATCH -e dcl_02.err
#SBATCH -n 1 --exclusive -p gpu2Q -q gpuq --gres=gpu:2
# (删除这一行)参数解释：-J 任务名，-o 输出记录文件名，-e 错误记录文件名，一般只要改这个

# CUDA环境
CUDA_VISIBLE_DEVICES=0,1
# 执行操作
python train.py
wait
```
2. 申请任务 `sbatch task.sh`
3. 查看任务队列 `squeue`
4. 进入显卡节点查看状态 `cd gpu**`，根据squeue分配的输入。查看GPU状态`nvidia-smi`
