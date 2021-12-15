# Helmchart repo for Whalebone tools

How to add repo?
1. Install the lastest vewrsion of HELM (https://helm.sh/)
2. Obtain Github Personal Access Token
3. Add repo using following commands:
  helm repo add --username <username> --password <token> whalebone "https://raw.githubusercontent.com/whalebone/helmcharts/main/"
4. helm search repo whalebone

  
  You should see list of charts:
  
  NAME           	CHART VERSION	APP VERSION	DESCRIPTION                                       
whalebone/test1	0.0.1        	0.0.1      	A test intallation of whalebone resolver in Kub...


 
  
