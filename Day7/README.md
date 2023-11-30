# Day 7 - Azure Artifacts


## Setup your Azure repos with the same application code

You can import the below repo to clone the Nike landing page sample website code to your Azure Repos:

https://github.com/piyushsachdeva/nike_landing_page.git


## Architectural diagram used in the video

![image](https://github.com/piyushsachdeva/AzureDevOps-Zero-to-Hero/assets/40286378/f7facb49-af0d-4f6a-8e14-ae8444423c91)

## Build Pipeline YAML code:

``` YAML
trigger: 
- main

stages:
- stage: Build
  jobs:
  - job: Build
    pool:
      vmImage: 'ubuntu-latest'
    steps:
    - task: Npm@1
      inputs:
        command: 'custom'
        customCommand: 'install -D tailwindcss postcss autoprefixer'
    - task: Npm@1
      inputs:
        command: 'custom'
        customCommand: 'run build'

    - task: Npm@1
      inputs:
        command: 'publish'
        workingDir: './dist'
        publishRegistry: 'useFeed'
        publishFeed: '$FEED_DETAILS'
```



### Post-deployment inline script in the Release pipeline

```
cp -rf /home/site/wwwroot/package/* /home/site/wwwroot/
```


