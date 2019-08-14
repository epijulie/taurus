# taurus

Needed to run taurus on the local machine for EpiAnalyst

Before running the scripts, `brew install taurus`

Save the JMX files from blazemeter, place them in the same folder as this repo.

Divided into three files
settings.yaml execution.yaml cloud.yaml

# settings.yaml
settings.yaml defines the environment and the variables that the tests will run in.
You can define TAURUS API keys in the settings.yaml if you want to send the tests to blazemeter

# execution.yaml
execution.yaml defines the file that Taurus will run 
* script: specific jmx file 
* variables: taken from settings.yaml
* concurrency: number of target concurrent virtual users
  - local: number of concurrent virtual users in the local machine
  - cloud: number of concurrent virtual users in blazemeter
* ramp-up: ramp-up time to reach target concurrency
* hold-for: time to hold target concurrency
* locations: determines which location the API calls will be made through blazemeter

Other settings can be found https://gettaurus.org/docs/ExecutionSettings/ 

You can run the tests by command: `bzt settings.yaml execution.yaml`

# cloud.yaml
When # provisioning: cloud, gets uncommented on execution.yaml, and called in the command, it will start cloud.yaml
* token: '${API_KEY}:${API_SECRET}'  # API id and API secret divided by :
* timeout: 10s  # BlazeMeter API client timeout
* browser-open: start  # auto-open browser on test start/end/both/none
* check-interval: 5s  # interval which Taurus uses to query test status from BlazeMeter
* public-report: false  # make test report public, disabled by default
* send-report-email: false  # send report email once test is finished, disabled by default

Cloud settings found in https://gettaurus.org/docs/Cloud/

Run the tests by command: `bzt settings.yaml execution.yaml cloud.yaml`
