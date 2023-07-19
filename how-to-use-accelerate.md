# How to use 🤗Accelerate for faster training

In order to use 🤗Accelerate for multi-GPU training,
user must run `$accelerate config` to generate default configuration.

After the configuration file is prepared, run

```bash
$ accelerate launch TRAINING_SCRIPT.py
```