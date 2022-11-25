CMSSW is a big and complex piece of multitheaded (using pthreads) software that is exremely modular. 
- CMSSW Input:
  - Python Configuration files where data sources and set of modules to be executed is given by the user. In addition, in this file, the user will provide how modules will be executed and their modules  dependencies. In addition, the user may request to execute the same configuration more than once (using same/different data sources)
- CMSSW step 1 (load and get ready): 
  - the CMSSW will extracted all required modules and data sources from configuration file. 
  - Modules will be loaded and data will be fetched (from files, database, ... etc).     
  - CMSSW will build a DAG (direct acyclic graph) from the modules and their dependencies. 
  - In case user would like to execute its configurations more than once, CMSSW will build seperate DAG for each execution (with same/different data sources.) 
  - For each DAG, the CMSSW will and event Queue (EQ) that will include only the root of the DAG (which is a module) and nothing else. 
- CMSSW Step 2 (Main part):
  - CMSSW will fetch a one module from EQ (where its input is ready) and assign it to an arbitrary thread to execute it. In somecases, a module my have more than one input and therefore all input must be ready before execution. 
  - The product of execution of the thread (which is data + following module according to DAG) will be stored back at EQ.
- CMSSW Step 3 (results): 
  - Once the EQ are all empty, the CMSSW will put back results as instructed by the user in the configuration file.   

NOTES: 
- CMSSW assumes a poll of thread is available to execute any ready module. A thread may run modules from the same/different DAG trees. 


For MPI Project
- We would like to run CMSSW on multiple processes. 
- The main process will be the one that start and finish the CMSSW run. 
- The worker process will communicate with another 
