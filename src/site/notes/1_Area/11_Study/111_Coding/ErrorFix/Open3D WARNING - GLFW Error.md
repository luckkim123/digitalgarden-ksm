---
{"dg-publish":true,"permalink":"/1-area/11-study/111-coding/error-fix/open3-d-warning-glfw-error/","tags":["Study/Coding/solution"],"noteIcon":"","created":"2024-07-09, 17:13"}
---

# 문제 발생
- Open3D 를 실행할 때 해당 문제 발생 시
	```bash
	[Open3D WARNING] GLFW Error: GLX: Failed to create context: BadMatch (invalid parameter attributes)
	[Open3D WARNING] Failed to create window
	[Open3D WARNING] [DrawGeometries] Failed creating OpenGL window.
	```

# 해결 방법
- Docker container 실행 시 다음 옵션 추가
	```bash
	--gpus 'all,"capabilities=compute,utility,graphics"'
	-v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY
	```

