---
title: "Resources"
revised: 2024
---

## Glossary

Here's a [Glossary](../glossary/) of some terms we've used in class. Please suggest additional terms to add!

## Coding Tips

- General: [How to be a Wizard](https://wizardzines.com/zines/wizard/)
- Learning Python
  - [roadmap.sh: Learn to become a modern Python developer](https://roadmap.sh/python)
  - [Kaggle: Learn Python Tutorials](https://www.kaggle.com/learn/python)
- Debugging
  - [A debugging manifesto](https://jvns.ca/blog/2022/12/08/a-debugging-manifesto/)
    - Longer version: [The Pocket Guide to Debugging](https://wizardzines.com/zines/debugging-guide/)
  - Python specific: Read the **end** of the traceback.

## Computing

To run a Hugging Face model on the lab machines on GPU, put the following in a Dockerfile in a new directory and follow the instructions in the comments.

```Dockerfile
# build with `sudo docker build -t transformers-pytorch-gpu-streamlit .`
# Note: the period at the end is important
# run with `sudo docker run -it  --gpus all -p 8501:8501 -p 8888:8888 -v /scratch:/scratch -v ~:/home transformers-pytorch-gpu-streamlit bash`
# this:
# - runs the container interactively
# - uses all GPUs
# - maps port 8501 on the host to port 8501 in the container
# - mounts /scratch on the host to /scratch in the container
# If you want to run a Jupyter notebook, you can also map port 8888 in the same way:
# `sudo docker run -it  --gpus all -p 8888:8888 -v /scratch:/scratch transformers-pytorch-gpu-streamlit jupyter notebook --allow-root --ip 0.0.0.0`
# You might want to allow the container to access your home directory, which you can do with `-v ~:/home`. But you'll probably need to have the container run as your user, which you can do with `-u $(id -u):$(id -g)`

FROM huggingface/transformers-pytorch-gpu
RUN pip install streamlit jupyter bitsandbytes 
RUN apt install wget; \
   wget https://vscode.download.prss.microsoft.com/dbazure/download/stable/e170252f762678dec6ca2cc69aba1570769a5d39/vscode_cli_alpine_x64_cli.tar.gz; \
   tar zxvf vscode_cli_alpine_x64_cli.tar.gz

# set the env var to make Hugging Face use the /scratch
ENV HF_HOME /scratch/cs344/huggingface
```


{{% details summary="`borg` Supercomputer" level="3" %}}

If you need more computing power or storage than the lab machines for your final projects, you can run on Borg.

To set up your environment, run `/storage/ArnoldGroup/anaconda3/bin/conda init`, then log off and log back on.

> Pro tip for accessing `borg`: put the following in `~/.ssh/config`
>
> ```
> Host borg
>     Hostname borg.calvin.edu
>     Port 22122
>     User YOUR_USERNAME
>     IdentityFile ~/.ssh/keys/borg OR WHEREVER YOUR KEY IS
> ```

The easiest way to use Borg is by running a training script from the command line. For example, you could make an `sbatch` script like this:

```bash
#!/bin/bash
#
# Run on the GPU node with one GPU, 4 CPUS, and 64GB of RAM
# Reserve one GPU
#SBATCH --gres=gpu:1
#
# Reserve four CPU cores
#SBATCH -c 4
#
# Reserve 64GB of RAM
#SBATCH --mem=64G
#
# Run in the GPUs queue
#SBATCH -p gpus

echo -n "Starting at "
date
echo "GPU info:"
nvidia-smi
which python
python -c 'import torch; print("PyTorch", torch.__version__, "CUDA=", torch.cuda.is_available())'

# Call the script here:
python training_script.py --input-data=... --batch-size=...

echo -n "Done at "
date
```

Then run it like `sbatch train_model.sbatch`.

If you need a notebook, please *don't* use the GPU node, because we only have 4 GPUs to share among all of us. Instead, use a compute node. Here's how to do it (could be more tested... let me know how it goes):

1. Get on a Linux machine (lab machine) unless you know what you're doing.
2. Set up an ssh keypair, where the lab machine has your private key and borg has the public key listed in `~/.ssh/authorized_keys`. Make sure permissions are set correctly: `chmod 700 ~/.ssh; chmod 600 ~/.ssh/authorized_keys`
3. Get a shell on a compute note: on borg, run `srun -c 2 --mem=64G  --pty bash`.
4. Note what machine you're on, e.g., `borg-node01` (the .calvin.edu part is optional).
5. Run `jupyter notebook --no-browser`.
6. On a second terminal on the lab machine, run `ssh -L 8888:borg-node01:8888 borg`. (replace the node name appropriately)
  
    There's a chance this might not work. If it fails, then in that second terminal instead just `ssh borg`, and then from there, `ssh -L8888:127.0.0.1:8888 borg-node01` or whatever node it is. Also, if you get a port number other than 8888 (because something else is using that port), use that port number in the commands above instead.

    Alternative: `ssh -J username@borg-node01 -L 8888:localhost:8888 borg`.

7. Back in the first terminal, copy and paste the link that `jupyter notebook` gave you into your web browser.

General instructions for using the [Slurm scheduler on Borg](https://borg.calvin.edu/resources-slurm.html)

{{% /details %}}

### Google Colab

Tips and Notes:

- If (and only if) you're working with images: Under the *Runtime* menu, select **Change runtime type** and select **GPU**. Otherwise many things will run very slowly.
- If you open a notebook from GitHub, **any changes are not saved**! Make sure you select "*Copy to Drive*" on the toolbar if you want to save changes.
- [intro](https://colab.research.google.com/notebooks/intro.ipynb), [overview](https://colab.research.google.com/notebooks/basic_features_overview.ipynb)
- Press Ctrl-Shift-P to open the Command Palette. Lots of useful stuff there; try the "scratch code cell".
- Click the down arrow next to the RAM/Disk meter in the toolbar (where it used to say "Connect") and select "show executed code history".

### Jupyter Notebook

-   [Appendix](https://nbviewer.jupyter.org/github/fastai/fastbook/blob/master/app_jupyter.ipynb) from our book
-   some [tips and tricks](https://github.com/NirantK/best-of-jupyter)
- If you're using git on the command line (instead of VS Code), you may appreciate `nbdiff`.

## Materials

- [Text and Image Generation](https://www.youtube.com/playlist?list=PLWfDJ5nla8UoG2mvvHs_OS0asAKC5HJeu) -- short and very clear YouTube videos
- [3blue1brown Linear Algebra](https://www.3blue1brown.com/topics/linear-algebra) articles with excellent videos

### Educational Materials

- [Deep Learning book](https://www.deeplearningbook.org/) by Goodfellow et al.
- ISLR [book](https://www.statlearning.com/) and [course](https://www.statlearning.com/online-course)
- [MIT 6.S191 Introduction to Deep Learning](http://introtodeeplearning.com/)
- Spring 2021 Videos for this class
  - Fundamentals 009 (Linear Regression with `Learner`) [walkthrough](https://www.youtube.com/playlist?list=PLYvyo-La3zBOvTxiOhy4y6l65TxcUtCuS)
  - [Lab 3 walkthrough](https://www.youtube.com/playlist?list=PLYvyo-La3zBN8qoyCf3l0RRaopUa0KXPG)
- Other Videos
  - [3Blue1Brown Neural Network Videos](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi)
  - [Art of the Problem - Deep Learning Playlist](https://www.youtube.com/playlist?list=PLbg3ZX2pWlgKV8K6bFJr5dhM7oOClExUJ): "Mathematics of Neural Networks" is a nice explanation of how neural nets use vector spaces.
- "Advice on getting started in deep learning" by Andrew Ng
- Deliberate practice. It's prerequisite to expertise. https://youtu.be/5eW6Eagr9XA?t=936 — I'll add: those four things are exactly what is needed for an AI to do something well also.

### Tools

- Git and GitHub
  - [GitHub's Git Handbook](https://guides.github.com/introduction/git-handbook/)
  - [Learn Git Branching](https://learngitbranching.js.org/?locale=en_US)
- Training Tips
  - <https://huggingface.co/blog/simple-considerations>
  - <http://josh-tobin.com/assets/pdf/troubleshooting-deep-neural-networks-01-19.pdf>
  - [A Recipe for Training Neural Networks](http://karpathy.github.io/2019/04/25/recipe/)
  - https://blog.floydhub.com/training-neural-nets-a-hackers-perspective/
- [RunwayML](https://runwayml.com/) (very high-level interface)
- Streamlit
- [WandB](https://wandb.ai/) (experiment tracking)

## Keeping up with AI

### Tech

-   [TWIML](https://twimlai.com/) -- podcast, blog
-   [Papers With Code](https://paperswithcode.com/) (sign up for the newsletter)
-   [Two Minute Papers](https://www.youtube.com/channel/UCbfYPyITQ-7l4upoX8nvctg) YouTube channel
-   [Arxiv-Sanity](http://www.arxiv-sanity.com/) (but still insane)
-   [distill.pub](https://distill.pub/)
-   [Harvard Data Science Review](https://hdsr.mitpress.mit.edu/)

### Ethics / Society

-   Fast.AI [Data Ethics course](https://ethics.fast.ai/)
-   [Montreal AI](https://montrealethics.ai/introduction-to-ethical-ai-principles/)
-   AI Now Institute
-   Data and Society
-   [The Oxford Handbook of Ethics of AI](https://global.oup.com/academic/product/the-oxford-handbook-of-ethics-of-ai-9780190067397?cc=ca&lang=en&#)
-   [Harvard BKC](https://twitter.com/BKCHarvard)
-   ACM Conference on Fairness, Accountability, and Transparency ([FAccT](https://facctconference.org/))
