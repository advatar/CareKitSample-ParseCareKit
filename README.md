# CareKitSample+ParseCareKit

An example application of [CareKit](https://github.com/carekit-apple/CareKit)'s OCKSample synchronizing with [ParseCareKit](https://github.com/netreconlab/ParseCareKit). 

The main branch uses a cocoapod version of CareKit that mirrors the CareKit master branch. The differences between the [pod](https://github.com/cbaker6/CareKit/tree/pod) branch and CareKits [master](https://github.com/carekit-apple/CareKit) can be seen [here](https://github.com/cbaker6/CareKit/pull/2). CareKit's master branch is currently limited to synching the following entities to Parse tables/classes:

- [x] OCKTask <-> Task
- [x] OCKOutcome <-> Outcome
- [x] OCKOutcomeValue <-> OutcomeValue
- [x] OCKScheduleElement <-> ScheduleElement
- [x] OCKNote <-> Note (For OCKTask, OCKOutcome, OCKOutcomeValue)
- [x] OCKRevisionRecord.KnowledgeVector <-> KnowledgeVector

If you would like to synchronize the missing CarKit's entities:

- [x] OCKPatient <-> Patient
- [x] OCKCarePlan <-> CarePlan
- [x] OCKContact <-> Contact

You should fork the [experimental branch](https://github.com/netreconlab/CareKitSample-ParseCareKit/tree/experimental) instead (Note that `OCKSample` uses `Contacts`, but doesn't use `OCKPatient` or `OCKContact`). The differences are in the [Podfile](https://github.com/netreconlab/CareKitSample-ParseCareKit/blob/87873cc1c9e35f46571ca340fbf8ec74baea0b70/Podfile#L9), specifically the `CareKitStore` pod. The main branch uses the [pod](https://github.com/cbaker6/CareKit/tree/pod) branch of CareKitStore while the experimental branch uses [pod_vector](https://github.com/cbaker6/CareKit/tree/pod_vector). The differences in the pod_vector branch from CareKit's master can be seen [here](https://github.com/cbaker6/CareKit/pull/1).


**Use at your own risk. There is no promise that this is HIPAA compliant and we are not responsible for any mishandling of your data**

## Setup Your Parse Server
You can setup your parse-server locally to test using [parse-hipaa](https://github.com/netreconlab/parse-hipaa). Simply type the following to get your parse-server running with postgres locally:

1. Fork [parse-hipaa](https://github.com/netreconlab/parse-hipaa)
2. `cd parse-hipaa`
3.  `docker-compose up` - this will take a couple of minutes to setup as it needs to initialize postgres, but as soon as you see `parse-server running on port 1337.`, it's ready to go. See [here](https://github.com/netreconlab/parse-hipaa#getting-started) for details.

## Fork this repo to get the modified OCKSample app. 

1. Fork [CareKitSample-ParseCareKit](https://github.com/netreconlab/ParseCareKit)
2. Open `OCKSample.xcworkspace` in Xcode
3. You may need to configure your "Team" and "Bundle Identifier" in "Signing and Capabilities"
4. Build the project. If you get any errors, type "pod update" in the project directory in Terminal
5. Run the app and data will synchronize with parse-hipaa via http://localhost:1337/parse automatically
6. You can edit Parse server setup in the ParseCareKit.plist file under "Supporting Filles" in the Xcode browser

## View your data in Parse Dashboard
Parse Dashboard is the easiest way to view your data in the Cloud (or local machine in this example) and comes with [parse-hipaa](https://github.com/netreconlab/parse-hipaa). To access:
1. Open your browser and go to http://localhost:4040/dashboard
2. Username: `parse`
3. Password: `1234`
4. Be sure to refresh your browser to see new changes synched from your CareKitSample app

Note that CareKit data is extremely sensitive and you are responsible for ensuring your parse-server meets HIPAA compliance.
