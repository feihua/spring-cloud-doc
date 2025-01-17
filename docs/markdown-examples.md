
```text
Nginx 的默认安装目录包括但不限于：

配置文件目录：/etc/nginx

主配置文件：/etc/nginx/nginx.conf

默认服务器根目录：/usr/share/nginx/html

日志文件目录：/var/log/nginx

默认的 PID 文件位置：/var/run/nginx.pid

二进制文件位置：/usr/sbin/nginx

相关命令： 
systemctl enable nginx
systemctl start nginx
systemctl status nginx
```

```text
location /api {
		proxy_set_header Host $host;
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header REMOTE-HOST $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_pass http://127.0.0.1:8600;
	}
```

```text
location ^~ /antd{
		alias html/antd;
		index index.html; 
		try_files $uri $uri/ /antd/index.html;
		}
		
```

jdk安装
```shell
export JAVA_HOME=/root/jdk
export CLASSPATH=$JAVA_HOME/lib:$CLASSPATH
export PATH=$JAVA_HOME/bin:$PATH
```
```shell
docker run --network=host --name jenkins -v jenkins_home:/var/jenkins_home -d jenkins/jenkins:lts

docker logs -f docker-jenkins

# 进去容器
docker exec -it docker-jenkins /bin/bash
# 获取解锁密码
cat /var/jenkins_home/secrets/initialAdminPassword

aaad6cc16374442ab8b3a8ee0d5c870a123

```

```shell
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
               sh 'echo clean package'
            }
        }
        stage('Build') {
            steps {
                sh 'echo clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'echo test'
            }
        }
        stage('Deploy') {
            steps {
                sh 'echo deployment.yaml'
            }
        }
    }
}

```

```shell
pipeline {
    agent any

    stages {
        stage('clone') {
            steps {
                sh 'git clone https://gitee.com/liufeihua/spring-cloud-tpl.git'
            }
        }
        stage('gradle build') {
            steps {
                sh './gradlew bootJart'
            }
        }
    }
}

```

# Markdown Extension Examples

This page demonstrates some of the built-in markdown extensions provided by VitePress.

## Syntax Highlighting

VitePress provides Syntax Highlighting powered by [Shiki](https://github.com/shikijs/shiki), with additional features like line-highlighting:

**Input**

````md
```js{4}
export default {
  data () {
    return {
      msg: 'Highlighted!'
    }
  }
}
```
````

**Output**

```js{4}
export default {
  data () {
    return {
      msg: 'Highlighted!'
    }
  }
}
```

## Custom Containers

**Input**

```md
::: info
This is an info box.
:::

::: tip
This is a tip.
:::

::: warning
This is a warning.
:::

::: danger
This is a dangerous warning.
:::

::: details
This is a details block.
:::
```

**Output**

::: info
This is an info box.
:::

::: tip
This is a tip.
:::

::: warning
This is a warning.
:::

::: danger
This is a dangerous warning.
:::

::: details
This is a details block.
:::

## More

Check out the documentation for the [full list of markdown extensions](https://vitepress.dev/guide/markdown).
