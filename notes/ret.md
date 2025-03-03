```
as3r@as3r-ThinkPad-X1-Carbon-3rd:~/AutonomousDriving/pylot/docker$ ./build_images.sh
[+] Building 94.0s (28/44)                                                                                                                                                                  docker:default
 => [internal] load build definition from Dockerfile                                                                                                                                                  0.0s
 => => transferring dockerfile: 4.21kB                                                                                                                                                                0.0s
 => WARN: MaintainerDeprecated: Maintainer instruction is deprecated in favor of using label (line 2)                                                                                                 0.0s
 => [internal] load metadata for docker.io/nvidia/cudagl:11.4.2-devel-ubuntu20.04                                                                                                                     2.2s
 => [internal] load .dockerignore                                                                                                                                                                     0.0s
 => => transferring context: 2B                                                                                                                                                                       0.0s
 => [ 1/41] FROM docker.io/nvidia/cudagl:11.4.2-devel-ubuntu20.04@sha256:28bfecb17a9f295124e985e575a84ba851cff435c23b48536e14406126ae4748                                                             0.0s
 => CACHED [ 2/41] RUN apt-get -y update && apt-get -y install sudo                                                                                                                                   0.0s
 => CACHED [ 3/41] RUN mkdir -p /home/erdos                                                                                                                                                           0.0s
 => CACHED [ 4/41] RUN groupadd erdos -g 1000                                                                                                                                                         0.0s
 => CACHED [ 5/41] RUN useradd -r -u 1000 -g erdos erdos                                                                                                                                              0.0s
 => CACHED [ 6/41] RUN echo "erdos ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/erdos                                                                                                                    0.0s
 => CACHED [ 7/41] RUN chmod 0440 /etc/sudoers.d/erdos                                                                                                                                                0.0s
 => CACHED [ 8/41] RUN chown 1000:1000 -R /home/erdos                                                                                                                                                 0.0s
 => CACHED [ 9/41] RUN usermod --shell /bin/bash erdos                                                                                                                                                0.0s
 => CACHED [10/41] WORKDIR /home/erdos                                                                                                                                                                0.0s
 => CACHED [11/41] RUN mkdir -p /home/erdos/workspace                                                                                                                                                 0.0s
 => CACHED [12/41] RUN cd /home/erdos/workspace                                                                                                                                                       0.0s
 => CACHED [13/41] RUN sudo apt-get -y update && sudo apt-get -y install --reinstall locales && sudo locale-gen en_US.UTF-8                                                                           0.0s
 => CACHED [14/41] RUN sudo apt-get -y --fix-missing update                                                                                                                                           0.0s
 => CACHED [15/41] RUN sudo DEBIAN_FRONTEND=noninteractive sudo DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata                                                                              0.0s
 => CACHED [16/41] RUN sudo apt-get -y install apt-utils git curl clang python-is-python3 python3-pip                                                                                                 0.0s
 => CACHED [17/41] RUN python3 -m pip install --upgrade pip -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com                                                               0.0s
 => CACHED [18/41] RUN python3 -m pip install setuptools setuptools-rust numpy==1.19.5 -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com                                    0.0s
 => CACHED [19/41] RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y                                                                                                        0.0s
 => CACHED [20/41] RUN echo "export PATH=/home/erdos/.cargo/bin:/home/erdos/.cargo/bin:/usr/local/nvidia/bin:/usr/local/cuda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin" >> ~/  0.0s
 => CACHED [21/41] RUN rustup default nightly                                                                                                                                                         0.0s
 => CACHED [22/41] RUN mkdir -p /home/erdos/workspace                                                                                                                                                 0.0s
 => CACHED [23/41] RUN pip3 install maturin -i https://mirrors.ustc.edu.cn/pypi/simple/                                                                                                               0.0s
 => CACHED [24/41] RUN cd /home/erdos/workspace && git clone --depth 1 https://github.com/erdos-project/erdos.git && cd erdos/python                                                                  0.0s
 => ERROR [25/41] RUN cd /home/erdos/workspace/erdos && maturin develop                                                                                                                              91.4s
------                                                                                                                                                                                                     
 > [25/41] RUN cd /home/erdos/workspace/erdos && maturin develop:                                                                                                                                          
90.72 💥 maturin failed                                                                                                                                                                                    
90.72   Caused by: Couldn't find a virtualenv or conda environment, but you need one to use this command. For maturin to find your virtualenv you need to either set VIRTUAL_ENV (through activate), set CONDA_PREFIX (through conda activate) or have a virtualenv called .venv in the current or any parent folder. See https://virtualenv.pypa.io/en/latest/index.html on how to use virtualenv or use `maturin build` and `pip install <path/to/wheel>` instead.
------
Dockerfile:51
--------------------
  49 |     ENV PATH="/home/erdos/.local/bin:$PATH"
  50 |     RUN cd /home/erdos/workspace && git clone --depth 1 https://github.com/erdos-project/erdos.git && cd erdos/python 
  51 | >>> RUN cd /home/erdos/workspace/erdos && maturin develop
  52 |     
  53 |     # Set up Pylot.
--------------------
ERROR: failed to solve: process "/bin/bash --login -c cd /home/erdos/workspace/erdos && maturin develop" did not complete successfully: exit code: 1
exit status 1
```