# Test Microphone

First, step is to list all available microphone devices:

```
sudo  arecord -l
```

Next record a short 10 seconds audio by using the following command:

```
sudo arecord -f S16_LE -d 10 -r 16000 --device="hw:1,0" /tmp/test-mic.wav
```

`--device="hw:1,0"` means in `card 1` and `device 0` from the `arecord -l` output in the previous step.

Now confirm that the microphone recorded correctly your audio input by using `aplay`:

```
aplay /tmp/test-mic.wav
```
