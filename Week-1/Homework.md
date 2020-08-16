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
### MiniCluster  
```
1 PD
3 TiKV 
1 TiDB
```
### Run PD
```
./bin/pd-server --name="minicluster" \
          --data-dir="/data/pd" \
          --client-urls="http://127.0.0.1::2379" \
          --peer-urls="http://127.0.01:2380" \
          --log-file=/data/pd/pd.log
```
### Run TiKV
```
./bin/tikv-server --pd-endpoints="127.0.0.1:2379" \
                --addr="127.0.0.1:20160" \
                --data-dir=/data/tikv1 \
                --log-file=/data/tikv1.log 

./bin/tikv-server --pd-endpoints="127.0.0.1:2379" \
                --addr="127.0.0.1:20161" \
                --data-dir=/data/tikv2 \
                --log-file=/data/tikv2.log 

./bin/tikv-server --pd-endpoints="127.0.01:2379" \
                --addr="127.0.0.1:20162" \
                --data-dir=/data/tikv3 \
                --log-file=/data/tikv3.log 

```

### Run TiDB
```
./bin/tidb-server --store=tikv --path="127.0.0.1:2379" --config ./config.toml
```