# P2L1TPFPLoadBalancing

Download input ROOT file and run notebook:
```bash
wget -O perfTuple_manosID.root https://www.dropbox.com/s/5pc87vab3r7o92k/perfTuple_manosID.root?dl=1
jupyter notebook
```

Or to rerun it yourself:
```bash
cmsrel CMSSW_10_5_0_pre1
cd CMSSW_10_5_0_pre1/src
cmsenv
git cms-init
git cms-checkout-topic -u p2l1pfp:L1PF_10_5_X_v3
git cms-merge-topic -u jmduarte:L1PF_10_5_X_v3
# scripts
git clone git@github.com:p2l1pfp/FastPUPPI -b 105X_v3
pushd FastPUPPI
git remote add jmgd git@github.com:jmduarte/FastPUPPI
git fetch jmgd
git merge jmgd/105X_v3
popd
scram b -j8
cd FastPUPPI/NtupleProducer/python/
cmsRun runPerformanceNTuple.py
```

Edit `runPerformanceNTuple.py` to run with or without `emVsPUID` and `emVsPionID`:
```python
# turn on emVsPUID and emVsPionID for HGCAL 3D clusters
process.pfClustersFromHGC3DClusters.emVsPionID.method = cms.string("BDT")
process.pfClustersFromHGC3DClusters.emVsPUID.method = cms.string("BDT")
```

```python
# turn off emVsPUID and emVsPionID for HGCAL 3D clusters
process.pfClustersFromHGC3DClusters.emVsPionID.method = cms.string("")
process.pfClustersFromHGC3DClusters.emVsPUID.method = cms.string("")
```
