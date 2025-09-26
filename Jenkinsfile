pipeline {
  agent any
  options {
        timeout(time: 4, unit: 'HOURS') 
    }   
  environment {
    APPSYSID = '47ca17d493507a94ca30b3b86cba100f'
    CREDENTIALS = 'servicenow'
    DEVENV = 'https://hclnowintelligence.service-now.com'
    PRODENV = 'https://ven03869.service-now.com'
    #TESTSUITEID = 'bf8c266d732333005ce769972bf6a777'
  }
    

stages {
    stage('Build') {
      steps {
        snApplyChanges(appSysId: "${APPSYSID}", url: "${DEVENV}", credentialsId: "${CREDENTIALS}")
        snPublishApp(credentialsId: "${CREDENTIALS}", url: "${DEVENV}", appSysId: "${APPSYSID}",
          isAppCustomization: true, obtainVersionAutomatically: true, incrementBy: 2)
          
       
        
      }
    }  
    
    stage('Install'){
           steps {
        snDevOpsChange()
       snInstallApp(credentialsId: "${CREDENTIALS}", url: "${PRODENV}", appSysId: "${APPSYSID}", baseAppAutoUpgrade: false)        
        
      }
    }
}

}
