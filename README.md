# Helmchart repo for Whalebone tools

How to add repo?
1. Install the lastest vewrsion of HELM (https://helm.sh/)
2. Obtain Github Personal Access Token
3. Add repo using following commands:
  helm repo add --username <username> --password <token> whalebone "https://raw.githubusercontent.com/whalebone/helmcharts/main/"
4. helm search repo whalebone --versions

  
  You should see list of charts:
  
  NAME           	CHART VERSION	APP VERSION	DESCRIPTION                                       
whalebone/wb-resolver	0.0.3        	0.0.1      	A test intallation of whalebone resolver in Kub...
whalebone/wb-resolver	0.0.2        	0.0.1      	A test intallation of whalebone resolver in Kub...
whalebone/wb-resolver	0.0.1        	0.0.1      	A test intallation of whalebone resolver in Kub...


How to install a chart:
helm install wb-resolver whalebone/wb-resolver -f ~/Github-Whalebone/gcp-sandbox-10/resolver/helm-values-files/dev1.yml
 
How to package a chart:
  helm package ./wb-resolver/
  helm repo index ./
Push to Github

How to remove a repo:
helm repo remove whalebone
