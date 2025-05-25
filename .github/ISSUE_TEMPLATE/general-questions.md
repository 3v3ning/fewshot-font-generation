---
name: General questions
about: Issues not related to bugs
title: 'lf 모델 관련 자소 분해 정보 파일 준비 관련 질문'
labels: ''
assignees: ''

---
(현재 진행 단계)
저희는 기존 깃허브 파일에 담긴 decomposition,primals 파일로 phase1학습을 진행하였습니다.
phase2에 대해서 자소 조합을 골고루 갖춘 172자에 대한 손글씨 이미지(png), 172자 목록에 대한 decomposition_2.json파일을 준비하였고
primals.json은 기존 깃허브 프로젝트에 담긴 파일을 사용하였습니다.
다음과 같이 준비한 172자 목록에 없는 '췸'이라는 단어에 대해 key에러가 발생합니다.
INFO::05/25 14:26:18 | Run Argv:
> train_LF.py cfgs/LF/p2/train.yaml cfgs/data/train/custom.yaml --resume result/lf_output/checkpoints/039880.pth --phase 2 --work_dir ./result/lf_phase2 --decomposition_path data/custom/decomposition_2.json
INFO::05/25 14:26:18 | Args:
config_paths  = ['cfgs/LF/p2/train.yaml', 'cfgs/data/train/custom.yaml']
phase         = 2
nodes         = 1
gpus_per_node = 1
nr            = 0
port          = 13481
verbose       = True
world_size    = 1
INFO::05/25 14:26:18 | Configs:
seed: 2
model: lf
phase: gen
decomposition: data/custom/decomposition_2.json
primals: data/kor/primals.json
max_iter: 25000
g_lr: 0.0002
d_lr: 0.0008
ac_lr: 0.0002
adam_betas: 
  - 0.0
  - 0.9
trainer: 
  resume: result/lf_output/checkpoints/039880.pth
  force_resume: True
  work_dir: result/lf_phase2
  pixel_loss_type: l1
  pixel_w: 0.1
  gan_w: 1.0
  fm_layers: all
  fm_w: 1.0
  ac_w: 0.1
  ac_gen_w: 0.1
  fact_const_w: 1.0
  save: all-last
  print_freq: 100
  val_freq: 100
  save_freq: 50
  tb_freq: 100
gen: 
  emb_dim: 8
dset: 
  loader: 
    batch_size: 1
    num_workers: 16
  train: 
    source_path: data/custom/style
    source_ext: png
    data_dir: data_example/kor/ttf
    chars: data/kor/train_chars.json
    extension: ttf
  val: 
    unseen_chars: 
      data_dir: data/custom/content
      extension: png
      n_gen: 20
      n_font: 1
      chars: data/custom/chars.json
      source_path: data/custom/style
      source_ext: png
    seen_chars: 
      data_dir: data/custom/content
      extension: png
      n_gen: 20
      n_font: 1
      chars: data/custom/chars.json
      source_path: data/custom/style
      source_ext: png
decomposition_path: data/custom/decomposition_2.json
use_ddp: False
2025-05-25 14:26:18.830692: E external/local_xla/xla/stream_executor/cuda/cuda_fft.cc:477] Unable to register cuFFT factory: Attempting to register factory for plugin cuFFT when one has already been registered
WARNING: All log messages before absl::InitializeLog() is called are written to STDERR
E0000 00:00:1748183178.851084   17196 cuda_dnn.cc:8310] Unable to register cuDNN factory: Attempting to register factory for plugin cuDNN when one has already been registered
E0000 00:00:1748183178.857408   17196 cuda_blas.cc:1418] Unable to register cuBLAS factory: Attempting to register factory for plugin cuBLAS when one has already been registered
2025-05-25 14:26:18.877694: I tensorflow/core/platform/cpu_feature_guard.cc:210] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX512F FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
INFO::05/25 14:26:23 | [0] Get dataset ...
/usr/local/lib/python3.11/dist-packages/torch/utils/data/dataloader.py:624: UserWarning: This DataLoader will create 16 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
  warnings.warn(
gd is excluded! (no available characters)
gd is excluded! (no available characters)
INFO::05/25 14:26:23 | [0] Build model ...
The weight is force overwrited.
INFO::05/25 14:26:24 | Resumed checkpoint from result/lf_output/checkpoints/039880.pth (Step 0)
INFO::05/25 14:26:24 | Start training ...
Traceback (most recent call last):
  File "/content/drive/.shortcut-targets-by-id/1olTIhbTlQ6UxJ-hMZI16B91s-ifwlXJJ/25-1AMDGroupE/project/font/train_LF.py", line 215, in <module>
    main()
  File "/content/drive/.shortcut-targets-by-id/1olTIhbTlQ6UxJ-hMZI16B91s-ifwlXJJ/25-1AMDGroupE/project/font/train_LF.py", line 211, in main
    train_single(args, cfg)
  File "/content/drive/.shortcut-targets-by-id/1olTIhbTlQ6UxJ-hMZI16B91s-ifwlXJJ/25-1AMDGroupE/project/font/train_LF.py", line 184, in train_single
    trainer.train(trn_loader, val_loaders, cfg.max_iter)
  File "/content/drive/.shortcut-targets-by-id/1olTIhbTlQ6UxJ-hMZI16B91s-ifwlXJJ/25-1AMDGroupE/project/font/LF/phase2_trainer.py", line 57, in train
    for batch in cyclize(loader):
  File "/content/drive/.shortcut-targets-by-id/1olTIhbTlQ6UxJ-hMZI16B91s-ifwlXJJ/25-1AMDGroupE/project/font/base/trainer/trainer_utils.py", line 16, in cyclize
    for x in loader:
  File "/usr/local/lib/python3.11/dist-packages/torch/utils/data/dataloader.py", line 708, in __next__
    data = self._next_data()
           ^^^^^^^^^^^^^^^^^
  File "/usr/local/lib/python3.11/dist-packages/torch/utils/data/dataloader.py", line 1480, in _next_data
    return self._process_data(data)
           ^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/local/lib/python3.11/dist-packages/torch/utils/data/dataloader.py", line 1505, in _process_data
    data.reraise()
  File "/usr/local/lib/python3.11/dist-packages/torch/_utils.py", line 733, in reraise
    raise exception
KeyError: Caught KeyError in DataLoader worker process 0.
Original Traceback (most recent call last):
  File "/usr/local/lib/python3.11/dist-packages/torch/utils/data/_utils/worker.py", line 349, in _worker_loop
    data = fetcher.fetch(index)  # type: ignore[possibly-undefined]
           ^^^^^^^^^^^^^^^^^^^^
  File "/usr/local/lib/python3.11/dist-packages/torch/utils/data/_utils/fetch.py", line 52, in fetch
    data = [self.dataset[idx] for idx in possibly_batched_index]
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/local/lib/python3.11/dist-packages/torch/utils/data/_utils/fetch.py", line 52, in <listcomp>
    data = [self.dataset[idx] for idx in possibly_batched_index]
            ~~~~~~~~~~~~^^^^^
  File "/content/drive/.shortcut-targets-by-id/1olTIhbTlQ6UxJ-hMZI16B91s-ifwlXJJ/25-1AMDGroupE/project/font/LF/phase2_dataset.py", line 127, in __getitem__
    (in_keys, in_chars, in_decs) = self.sample_input(self.n_in_c, self.n_in_s)
                                   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/content/drive/.shortcut-targets-by-id/1olTIhbTlQ6UxJ-hMZI16B91s-ifwlXJJ/25-1AMDGroupE/project/font/LF/phase2_dataset.py", line 63, in sample_input
    picked_decs += [self.decompose_to_ids(char)] * n_in_s
                    ^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/content/drive/.shortcut-targets-by-id/1olTIhbTlQ6UxJ-hMZI16B91s-ifwlXJJ/25-1AMDGroupE/project/font/LF/phase2_dataset.py", line 47, in decompose_to_ids
    comps = self.decomposition[char]
            ~~~~~~~~~~~~~~~~~~^^^^^^
KeyError: '췸'

반대로 1차 학습때 사용한 전체 한글에 대한 귀하의 팀에서 제공하는 decomposition.json을 이용하여 학습을 진행시
다음과 같이 특정 이미지 파일이 없다고 뜹니다.
INFO::05/25 13:46:29 | Run Argv:
> train_LF.py cfgs/LF/p2/train.yaml cfgs/data/train/custom.yaml --resume result/lf_output/checkpoints/039880.pth --phase 2 --work_dir ./result/lf_phase2 --decomposition_path data/kor/decomposition.json
INFO::05/25 13:46:29 | Args:
config_paths  = ['cfgs/LF/p2/train.yaml', 'cfgs/data/train/custom.yaml']
phase         = 2
nodes         = 1
gpus_per_node = 1
nr            = 0
port          = 13481
verbose       = True
world_size    = 1
INFO::05/25 13:46:29 | Configs:
seed: 2
model: lf
phase: gen
decomposition: data/kor/decomposition.json
primals: data/kor/primals.json
max_iter: 25000
g_lr: 0.0002
d_lr: 0.0008
ac_lr: 0.0002
adam_betas: 
  - 0.0
  - 0.9
trainer: 
  resume: result/lf_output/checkpoints/039880.pth
  force_resume: True
  work_dir: result/lf_phase2
  pixel_loss_type: l1
  pixel_w: 0.1
  gan_w: 1.0
  fm_layers: all
  fm_w: 1.0
  ac_w: 0.1
  ac_gen_w: 0.1
  fact_const_w: 1.0
  save: all-last
  print_freq: 100
  val_freq: 100
  save_freq: 50
  tb_freq: 100
gen: 
  emb_dim: 8
dset: 
  loader: 
    batch_size: 1
    num_workers: 16
  train: 
    source_path: data/custom/style
    source_ext: png
    data_dir: data_example/kor/ttf
    chars: data/kor/train_chars.json
    extension: ttf
  val: 
    unseen_chars: 
      data_dir: data/custom/content
      extension: png
      n_gen: 20
      n_font: 1
      chars: data/custom/chars.json
      source_path: data/custom/style
      source_ext: png
    seen_chars: 
      data_dir: data/custom/content
      extension: png
      n_gen: 20
      n_font: 1
      chars: data/custom/chars.json
      source_path: data/custom/style
      source_ext: png
decomposition_path: data/kor/decomposition.json
use_ddp: False
2025-05-25 13:46:30.470840: E external/local_xla/xla/stream_executor/cuda/cuda_fft.cc:477] Unable to register cuFFT factory: Attempting to register factory for plugin cuFFT when one has already been registered
WARNING: All log messages before absl::InitializeLog() is called are written to STDERR
E0000 00:00:1748180790.492468    6697 cuda_dnn.cc:8310] Unable to register cuDNN factory: Attempting to register factory for plugin cuDNN when one has already been registered
E0000 00:00:1748180790.498736    6697 cuda_blas.cc:1418] Unable to register cuBLAS factory: Attempting to register factory for plugin cuBLAS when one has already been registered
2025-05-25 13:46:30.519896: I tensorflow/core/platform/cpu_feature_guard.cc:210] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX512F FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
INFO::05/25 13:46:34 | [0] Get dataset ...
/usr/local/lib/python3.11/dist-packages/torch/utils/data/dataloader.py:624: UserWarning: This DataLoader will create 16 worker processes in total. Our suggested max number of worker in current system is 2, which is smaller than what this DataLoader is going to create. Please be aware that excessive worker creation might get DataLoader running slow or even freeze, lower the worker number to avoid potential slowness/freeze if necessary.
  warnings.warn(
gd is excluded! (no available characters)
gd is excluded! (no available characters)
INFO::05/25 13:46:34 | [0] Build model ...
The weight is force overwrited.
INFO::05/25 13:46:35 | Resumed checkpoint from result/lf_output/checkpoints/039880.pth (Step 0)
INFO::05/25 13:46:35 | Start training ...
Traceback (most recent call last):
  File "/content/drive/.shortcut-targets-by-id/1olTIhbTlQ6UxJ-hMZI16B91s-ifwlXJJ/25-1AMDGroupE/project/font/train_LF.py", line 215, in <module>
    main()
  File "/content/drive/.shortcut-targets-by-id/1olTIhbTlQ6UxJ-hMZI16B91s-ifwlXJJ/25-1AMDGroupE/project/font/train_LF.py", line 211, in main
    train_single(args, cfg)
  File "/content/drive/.shortcut-targets-by-id/1olTIhbTlQ6UxJ-hMZI16B91s-ifwlXJJ/25-1AMDGroupE/project/font/train_LF.py", line 184, in train_single
    trainer.train(trn_loader, val_loaders, cfg.max_iter)
  File "/content/drive/.shortcut-targets-by-id/1olTIhbTlQ6UxJ-hMZI16B91s-ifwlXJJ/25-1AMDGroupE/project/font/LF/phase2_trainer.py", line 57, in train
    for batch in cyclize(loader):
  File "/content/drive/.shortcut-targets-by-id/1olTIhbTlQ6UxJ-hMZI16B91s-ifwlXJJ/25-1AMDGroupE/project/font/base/trainer/trainer_utils.py", line 16, in cyclize
    for x in loader:
  File "/usr/local/lib/python3.11/dist-packages/torch/utils/data/dataloader.py", line 708, in __next__
    data = self._next_data()
           ^^^^^^^^^^^^^^^^^
  File "/usr/local/lib/python3.11/dist-packages/torch/utils/data/dataloader.py", line 1480, in _next_data
    return self._process_data(data)
           ^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/local/lib/python3.11/dist-packages/torch/utils/data/dataloader.py", line 1505, in _process_data
    data.reraise()
  File "/usr/local/lib/python3.11/dist-packages/torch/_utils.py", line 733, in reraise
    raise exception
FileNotFoundError: Caught FileNotFoundError in DataLoader worker process 0.
Original Traceback (most recent call last):
  File "/usr/local/lib/python3.11/dist-packages/torch/utils/data/_utils/worker.py", line 349, in _worker_loop
    data = fetcher.fetch(index)  # type: ignore[possibly-undefined]
           ^^^^^^^^^^^^^^^^^^^^
  File "/usr/local/lib/python3.11/dist-packages/torch/utils/data/_utils/fetch.py", line 52, in fetch
    data = [self.dataset[idx] for idx in possibly_batched_index]
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/local/lib/python3.11/dist-packages/torch/utils/data/_utils/fetch.py", line 52, in <listcomp>
    data = [self.dataset[idx] for idx in possibly_batched_index]
            ~~~~~~~~~~~~^^^^^
  File "/content/drive/.shortcut-targets-by-id/1olTIhbTlQ6UxJ-hMZI16B91s-ifwlXJJ/25-1AMDGroupE/project/font/LF/phase2_dataset.py", line 151, in __getitem__
    src_imgs = torch.cat([self.transform(self.read_source(c)) for c in trg_chars])
                         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/content/drive/.shortcut-targets-by-id/1olTIhbTlQ6UxJ-hMZI16B91s-ifwlXJJ/25-1AMDGroupE/project/font/LF/phase2_dataset.py", line 151, in <listcomp>
    src_imgs = torch.cat([self.transform(self.read_source(c)) for c in trg_chars])
                                         ^^^^^^^^^^^^^^^^^^^
  File "/content/drive/.shortcut-targets-by-id/1olTIhbTlQ6UxJ-hMZI16B91s-ifwlXJJ/25-1AMDGroupE/project/font/LF/phase2_dataset.py", line 43, in read_source_img
    img = Image.open(str(self.source / f"{char}.{self.source_ext}"))
          ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/local/lib/python3.11/dist-packages/PIL/Image.py", line 3505, in open
    fp = builtins.open(filename, "rb")
         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
FileNotFoundError: [Errno 2] No such file or directory: 'data/custom/style/싸.png'

오래 전에 마감하신 프로젝트여서 번거로우시겠지만 도움 주시면 감사하겠습니다.ㅜㅜ
<!-- Note that the quality of the generated images are usually not a bug, but limitation of our work. Also, if you want to use this work as your own font generator, please consider to use other repositories. This work is an academic work, not considering all the factors in real-world. We will close an issue that just complains about the generated quality. -->

<!-- Our work is for "few-shot font generation". It means that we train a model with a number of font libraries and then generate a new font with very small number of references (e.g., 8). Therefore, if your case is not the same this case, we will close the issue. You may have tried to work with your custom training fonts. Please check the other issues before upload the issue -->

<!-- LF-Font and MX-Font are based on "compositionally" of languages. For Chinese, we use https://commons.wikimedia.org/wiki/Commons:Chinese_characters_decomposition for the decomposition. If your character is not here, then our decomposition module will not work correctly. It is not a bug, therefore please make your own decomposition mappings. -->
