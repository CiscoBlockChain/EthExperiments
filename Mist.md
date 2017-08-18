## 1. first of all we run this block of instructions:

 `$ curl https://install.meteor.com/ | sh`

 `$ curl -o- -L https://yarnpkg.com/install.sh | bash`

 `$ yarn global add electron@1.4.15`

 `$ yarn global add gulp`
	
2.Then we intialise mist for development:

 `$ git clone https://github.com/ethereum/mist.git`

 `$ yarn`
	
3.In a new terminal window we start the interface with a Meteor server for autoreload:

 `$ cd mist/interface && meteor --no-release-check `

4.Here we added the port "10.100.2.204:3000" in the end of the previous instruction

 `$ cd mist/interface && meteor --no-release-check --port 10.100.2.204:3000`

5.In the original window we apply:

  `$ cd mist`
  `$ electron`
