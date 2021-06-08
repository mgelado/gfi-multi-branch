// Pipeline declarativo
pipeline {
    
    // Ejecutar el pipeline desde cualquier agente (nodo maquina) disponible
  agent {
    node {
      label 'principal'
    }
  }
   
  options {
    // Ficheros de log
    buildDiscarder logRotator (
      daysToKeepStr: '15', 
      numToKeepStr: '10'
    )
  }
  
  // Definicion de fases
  stages {
        
        stage('Cleanup Workspace') {
                        
            // Conjunto de pasos que componen la fase
            steps {
                cleanWs()
                echo 'Eliminado Workspace para Job';                
            }
        }  
      
      stage('Code Checkout') {
                        
            steps {
               checkout(
                $class: 'GitSCM', 
                 branches: [[name: '*/main']],
                 userRemoteConfigs: [[url: 'https://github.com/spring-projects/spring-petclinic.git']]
               )                
            }
        }  
      
    stage('Unit Testing') {
            
          when {
        branch 'testing'
      }
      
            steps {                
                echo 'Running Unit Tests';                
            }
        }  
    
     stage('Code Analysis') {
            
            steps {                
                echo 'Running Code Analysis';                
            }
        } 
    
    stage('Build Deploy code') {
      
      when {
        branch 'developer'
      }
      
      
      steps {                
        echo 'Building Artifact';    
            
        echo 'Deploying Code';
      }
    } 
  }    
}
