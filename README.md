# QCER_GenerateReader
Part of generate reader for QCER

**环境配置**

```
conda create -n 虚拟环境名称 python=3.8
pip install torch==1.8.1+cu111 -f https://download.pytorch.org/whl/torch_stable.html
pip install transformers==3.0.2
```

**（1）如何进行reader Inference?**

```
我的目标是什么？
用pyserini的检索结果（BM25，DPR，hybrid作为输入，第一次要用hybrid的结果）作为reader的输入
经过处理成为符合要求的输入后送入reader，获取reader的前5个predictions（先用base 版本的，所以只需要reader的PTMs进行推理就行了，其他的暂时不需要好吧，那就暂时不用管）

python test_reader.py \
        --model_path checkpoint_dir/my_experiment/my_model_dir/checkpoint/best_dev \
        --eval_data eval_data.json \
        --per_gpu_batch_size 1 \
        --n_context 100 \
        --name my_test \
        --checkpoint_dir checkpoint \
        
      
python reader_test.py --model_path /home/zhangxy/QA/FID-main/pretrained_models/nq_reader_base --eval_data /home/zhangxy/QA/FID-main/download/nq/run.dpr.nq-test.hybrid.json --per_gpu_batch_size 16 --n_context 1 --name nq_base_test --write_results
```



```
在FID-main/src/model.py line:55 的generate()模型中添加两个参数
num_beams=6
num_return_sequences=5

num_beams一定要大于num_return_sequences，否则会报错
```
