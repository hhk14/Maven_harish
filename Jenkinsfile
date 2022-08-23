pipeline
{
  agent any
  stages
  {
    stage('continuous download')
    {
      steps
      {
        git 'https://github.com/keshavr21/maven_test.git'
      }
    }
    stage('continuous build')
    {
      steps
      {
        sh '"/tmp/maven3/bin/mvn" clean package'
      }
    }
    stage('continuous deploy') 
    {
      steps
      {
        deploy adapters: [tomcat9(credentialsId: 'fe13aab6-83ee-4b2a-a044-1b6794258e35', path: '', url: 'http://172.31.45.167:8090/')], contextPath: 'scripted_pipeline_demo', war: '**/*.war'
      }
    }
    stage('continuous testing')
    {
      steps
      {
        git 'https://github.com/keshavr21/test_cases.git'
        sh 'java -jar testing.jar webapp/target/webapp.war'
      }
    }
    stage('continuous delivery')
    {
      steps
      {
        deploy adapters: [tomcat9(credentialsId: 'fe13aab6-83ee-4b2a-a044-1b6794258e35', path: '', url: 'http://172.31.45.167:8090/')], contextPath: 'scripted_pipeline_prod', war: '**/*.war'
      }
    }

    
  }
}
