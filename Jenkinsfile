//**************************************************************//
//    Inicio de pipeline
//**************************************************************//
//    Stage de primer cálculo '1stCalc'
//**************************************************************//
stage ('1stCalc') 
{
    //echo 'reiniciamos richweb y limpiamos caches... '
    //build job:'(MX_CL) Rich AUXILIAR - 40005', wait:true
    
     
	build job:'taskCalcExecution', wait:true
	echo 'Cálculo ejecutado correctamente....'
	echo 'mejoras pendientes: sacar alguna info del resultado de la ejecución '
	
	build job: 'Stoplight',propagate:false,wait:true,parameters: 
	[string(name: 'PATH', value: 'C:\\xmlPnet\\temp'),
	string(name: 'FILE', value: 'StepDone.0001')];

//**************************************************************//
//    Stage de primera extracción de datos '1stExtract'
//**************************************************************//
	stage('1stExtract'){
		echo '1stExtract'
		
		build job:'1stExtract', wait:true
		
		build job: 'Stoplight',propagate:false,wait:true,parameters: 
		[string(name: 'PATH', value: 'C:\\xmlPnet\\temp'),
		string(name: 'FILE', value: 'StepDone.0003')];
		
//**************************************************************//
//    Stage de instalación de mdbs en entorno 'packInstallation'
//**************************************************************//
		stage('PackInstalation'){
			build job:'PackInstalation', wait:true			
			echo 'Se han instalados todos los paquetes'
			echo 'mejoras pendientes: colocar log de paquetes instalados y alguna cosa mas.... '
	
        	build job: 'Stoplight',propagate:false,wait:true,parameters: 
        	[string(name: 'PATH', value: 'C:\\xmlPnet\\temp'),
        	string(name: 'FILE', value: 'StepDone.0002')];			
            
//**************************************************************//
//    Stage de segunda ejecución del cálculo '2ndCalc'
//**************************************************************//
			stage('2ndCalc'){
			//*******************************************************//
			//	Reiniciamos Rich y limpiamos caches
			//*******************************************************//
           //     echo 'reiniciamos richweb y limpiamos caches... '
           //     build job:'(MX_CL) Rich AUXILIAR - 40005', wait:true
                
                
            //*******************************************************//
			//	Ejecutamos segundo cálculo.
			//*******************************************************//				
                build job:'taskCalcExecution', wait:true
                echo 'Cálculo ejecutado correctamente....'
                echo 'mejoras pendientes: sacar alguna info del resultado de la ejecucion '
                	
            	build job: 'Stoplight',propagate:false,wait:true,parameters: 
            	[string(name: 'PATH', value: 'C:\\xmlPnet\\temp'),
            	string(name: 'FILE', value: 'StepDone.0001')];	
                
//**************************************************************//
//    Stage de segunda extracción de datos '2ndExtract'
//**************************************************************//				
			    stage('2ndExtract'){	
					echo '2ndExtract'

					build job:'1stExtract', wait:true
					
					build job: 'Stoplight',propagate:false,wait:true,parameters: 
					[string(name: 'PATH', value: 'C:\\xmlPnet\\temp'),
					string(name: 'FILE', value: 'StepDone.0004')];
		
//**************************************************************//
//    Stage de ejecutar comparación 'exeComparison'
//**************************************************************//		
					stage('exeComparison'){
						echo 'exeComparison'

						build job:'Analisis', wait:true
						
						build job: 'Stoplight',propagate:false,wait:true,parameters: 
						[string(name: 'PATH', value: 'C:\\xmlPnet\\temp'),
						string(name: 'FILE', value: 'StepDone.0005')];
									
//**************************************************************//
//    Stage de publicación de resultados 'publishResults'
//**************************************************************//								
						stage('publishResults'){
								echo 'publishResults'
								
								
						}
					
					}
					
				
				}
				
				
			}
			
		}
		
	}

}								

