### NVIDIA Docker

	# If you have nvidia-docker 1.0 installed: we need to remove it and all existing GPU containers
	docker volume ls -q -f driver=nvidia-docker | xargs -r -I{} -n1 docker ps -q -a -f volume={} | xargs -r docker rm -f
	sudo apt-get purge -y nvidia-docker

https://devblogs.nvidia.com/nvidia-docker-gpu-server-application-deployment-made-easy/


