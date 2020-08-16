## TiKV
# Build 

We build v4.0.4 TiDB 

### TiKV

1. Clone source code from github  https://github.com/tikv/tikv.  <br> Checkout tag v4.0.4.
2. Prepare Rust nightly environment <br>`$ curl -s https://static.rust-lang.org/rustup.sh | sh -s -- --channel=nightly`
3. Compile TiKV <br>`cd $SRC_TiKV; cargo build`

## PD & TiDB
### Build
1. Clone source code https://github.com/pingcap/tidb & https://github.com/pingcap/pd <br>Checkout tag v4.0.4. 
2. Setup golang 
3. Compile PD <br> `cd $SRC_PD; make`
4. Compile TiDB <br> `cd $SRC_TiDB; make`



## Deploy 
MiniCluster  
```
1 PD
3 TiKV 
1 TiDB
```