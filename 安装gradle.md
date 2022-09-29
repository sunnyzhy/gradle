# 安装 gradle

[gradle 官网](https://gradle.org/releases/ 'gradle 官网')

## 安装

1. 下载 ```binary-only```
2. 解压到任意目录并重命名，比如: ```D:\develop\gradle```
3. 配置环境变量:
   1. 新建系统变量，名称: ```GRADLE_HOME```; 值: ```D:\develop\gradle```
   2. 在 ```Path``` 里添加 ```%GRADLE_HOME%\bin```
   3. 自定义本地仓库。新建系统变量，名称: ```GRADLE_USER_HOME```; 值: ```D:\repository-gradle```
4. 执行 ```gradle -v```，如果出现版本信息即安装成功

## 配置阿里云镜像

在 ```D:\develop\gradle\init.d``` 目录下新建 ```init.gradle```，内容如下:

```gradle
allprojects{
    repositories {
        def ALIYUN_REPOSITORY_URL = 'https://maven.aliyun.com/repository/central/'
        def ALIYUN_JCENTER_URL = 'https://maven.aliyun.com/repository/public/'
        all { ArtifactRepository repo ->
            if(repo instanceof MavenArtifactRepository){
                def url = repo.url.toString()
                if (url.startsWith('https://repo1.maven.org/maven2') || url.startsWith('http://repo1.maven.org/maven2')) {
                    project.logger.lifecycle "Repository ${repo.url} replaced by $ALIYUN_REPOSITORY_URL."
                    remove repo
                }
                if (url.startsWith('https://jcenter.bintray.com/') || url.startsWith('http://jcenter.bintray.com/')) {
                    project.logger.lifecycle "Repository ${repo.url} replaced by $ALIYUN_JCENTER_URL."
                    remove repo
                }
            }
        }
        maven {
            url ALIYUN_REPOSITORY_URL
            url ALIYUN_JCENTER_URL
            url 'https://maven.aliyun.com/repository/google/'
            url 'https://maven.aliyun.com/repository/gradle-plugin/'
        }
    }
 
 
    buildscript{
        repositories {
            def ALIYUN_REPOSITORY_URL = 'https://maven.aliyun.com/repository/central/'
            def ALIYUN_JCENTER_URL = 'https://maven.aliyun.com/repository/public/'
            all { ArtifactRepository repo ->
                if(repo instanceof MavenArtifactRepository){
                    def url = repo.url.toString()
                    if (url.startsWith('https://repo1.maven.org/maven2') || url.startsWith('http://repo1.maven.org/maven2')) {
                        project.logger.lifecycle "Repository ${repo.url} replaced by $ALIYUN_REPOSITORY_URL."
                        remove repo
                    }
                    if (url.startsWith('https://jcenter.bintray.com/') || url.startsWith('http://jcenter.bintray.com/')) {
                        project.logger.lifecycle "Repository ${repo.url} replaced by $ALIYUN_JCENTER_URL."
                        remove repo
                    }
                }
            }
            maven {
                url ALIYUN_REPOSITORY_URL
                url ALIYUN_JCENTER_URL
                url 'https://maven.aliyun.com/repository/google/'
                url 'https://maven.aliyun.com/repository/gradle-plugin/'
            }
        }
    }
}
```
