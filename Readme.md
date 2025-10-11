برای اتصال اولاما به گرافیک کارت ابتدا پکیج های زیر را نصب کرده و سپس داکر را ری استارت میکنیم. سپس در داکر کمپوز، کارت گرافیک را معرفی میکنیم

sudo apt-get update
sudo apt-get install -y nvidia-container-toolkit
sudo systemctl restart docker

services:
  ollama:
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: all
              capabilities: [gpu]
    # for non-swarm mode, add this instead of deploy:
    runtime: nvidia

Unknown or Invalid Runtime Name: Nvidia    برای حل خطا 
    /etc/docker/daemon.json
    را ویرایش میکنیم و 
    
{
    "runtimes": {
        "nvidia": {
            "path": "nvidia-container-runtime",
            "runtimeArgs": []
        }
    }
}
به آن اضافه میکنیم
