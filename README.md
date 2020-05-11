Recovered after being deleted accidentally. 

__Basic Command__ to run the code:


_./waf --run "lpihandshake --paramter1 --parameter2"_

__List of Parameters__

- initialFlowCount: number of flows when the simulation starts .__Deafult__ 0
- simstop: simulation time
- k: value of k in a K-  ary fat tree. Details: https://www.cs.cornell.edu/courses/cs5413/2014fa/lectures/08-fattree.pdf
- enableCustomRouting: __false__ for ecmp __true__ for custom routing similar to what we have used here (https://www.researchgate.net/publication/331016143_Coordinated_Power_Management_in_Data_Center_Networks). For this paper we only considered ecmp (__enableCustomRouting = false__)
- enableMarkovMode: __true__ if traffic generation follows 2 state markov chain model (state 1 and state 2). __false__ otherwise
- markovETA0 and markovETA1: probability of creating one flow when some flow ends at state 1 and state 2 respectively. range: __[0,1]__ 
- enableTickModel: __true__ if traffic generation follows exponential distribution. In this paper, we used Tick model.
- tickInterval: Mean of the interflow arrival interval in Millisecond. It determines the overall utilization of the data center environment with specific link bandwidth, mean flow bandwidth and __k__ value. Details in paper. 
- enableOptimizer: __true__ to run the experiment with incremental optimization enabled, __false__ otherwise.
- uniformBursts: __true__ in order to change the mean flow bandwidth with some magnitude (it's hard coded need to convert it to cmd arguments, function name *FatTreeTopology::SetUpIntensityPhraseChangeVariables* in *ss-fat-tree-topology.cc* file). We used it to incorporate the burst situation in the experiment. __false__ for no burst at all. 
- RWratio: read write ratio for the experiment, range: __[0,1]__. 1 means 100 % read and 0 means 100% write. 
- deviceQDepth: no use at all in this work, can be ignored.

__Sample command__


*./waf --run "lpihandshake --initialFlowCount=0 --simStop=1 --k=6 --enableCustomRouting=false --enableMarkovModel=false --markovETA0=1 --markovETA1=0 --enableTickModel=true --tickInterval=1.38 --deviceQDepth=1000000 --enableOptimizer=true --uniformBursts=true --RWratio=0.9  --enableCopy=0"*
