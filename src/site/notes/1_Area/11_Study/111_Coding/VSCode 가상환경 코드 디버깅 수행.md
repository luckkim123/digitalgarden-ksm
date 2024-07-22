---
{"dg-publish":true,"permalink":"/1-area/11-study/111-coding/vs-code/","tags":["Study/Coding/VSCode"]}
---

- 실행하고자 하는 코드가 있는 프로젝트 폴더에 `launch.json` 과 `settings.json` 파일 생성
	```json title:launch.json
	{
		"version": "0.2.0",
		"configurations": [
			{
			"name": "Python: Current File",
			"type": "debugpy",
			"request": "launch",
			"args": ["--config","test.yaml",
				"--input","check.txt",
			], // argument 집어넣어서 실행할 경우
			"console": "integratedTerminal"
			}
		]
	}
	```
	
	```json title:settings.json
	{
		"python.testing.unittestArgs": [
			"-v",
			"-s",
			".",
			"-p",
			"test_*.py"
		],
		"python.testing.pytestEnabled": false,
		"python.testing.nosetestsEnabled": false,
		"python.testing.unittestEnabled": true,
		"python.pythonPath": "/workspace/project/calibration/.venv/bin/python3.10"
	}
	```