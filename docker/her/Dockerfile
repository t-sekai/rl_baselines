FROM tsekai/baselines_base:latest
ARG MAMBA_DOCKERFILE_ACTIVATE=1

ARG LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/root/.mujoco/mjpro150/bin"
ARG LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/root/.mujoco/mujoco200/bin"
ARG LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/root/.mujoco/mujoco210/bin"
ARG LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/lib/nvidia-430"


RUN ln -s /usr/lib/nvidia /usr/lib/nvidia-430
RUN mkdir /root/.mujoco && mkdir /root/.datasets && mkdir /work/mjrl
COPY .mujoco /root/.mujoco
COPY .datasets /root/.datasets
COPY mjrl /work/mjrl
RUN apt-get update && apt-get -y install patchelf libosmesa6-dev libgl1-mesa-glx libglfw3 libglew-dev
RUN pip install --upgrade pip && pip install "cython<3" && pip install cffi && pip install lockfile && pip install gdown && /bin/micromamba install -c conda-forge mesalib glew glfw
RUN pip install -e mjrl && pip install mujoco_py==2.0.2.8 && pip install -e mjrl/mj_envs