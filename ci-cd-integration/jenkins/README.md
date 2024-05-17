# Jenkins example for Deepfence YaRadare

This project demonstrates using Deepfence YaRadare in Jenkins build pipeline.
After customer's image is built, Deepfence YaRadare is run on the image and Malware results are either shown in STDOUT(build logs) or in a JSON file.
Refer [this](https://github.com/khulnasoft-lab/YaraHunter#command-line-options) for command line options


## Steps
- Ensure `khulnasoft/khulnasoft-yaradare:latest` image is present in the vm where jenkins is installed.
```shell script
docker pull khulnasoft/khulnasoft-yaradare:latest
```
### Scripted Pipeline
```
    stage('Run Deepfence YaRadare'){
        DeepfenceAgent = docker.image("khulnasoft/khulnasoft-yaradare:latest")
        try {
            c = DeepfenceAgent.run("--name=khulnasoft-yaradare -v /var/run/docker.sock:/var/run/docker.sock", "--image-name ${full_image_name}")
            sh "docker logs -f ${c.id}"
            def out = sh script: "docker inspect ${c.id} --format='{{.State.ExitCode}}'", returnStdout: true
            sh "exit ${out}"
        } finally {
            c.stop()
        }
    }
```
### Declarative Pipeline
```
stage('Run Deepfence Vulnerability Mapper'){
    steps {
        script {
            DeepfenceAgent = docker.image("khulnasoft/khulnasoft-yaradare:latest")
            try {
                c = DeepfenceAgent.run("--name=khulnasoft-yaradare -v /var/run/docker.sock:/var/run/docker.sock", "--image-name ${full_image_name}")
                sh "docker logs -f ${c.id}"
                def out = sh script: "docker inspect ${c.id} --format='{{.State.ExitCode}}'", returnStdout: true
                sh "exit ${out}"
            } finally {
                c.stop()
            }
        }
    }
}
```