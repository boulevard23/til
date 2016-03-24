# Use Xdebug on PHP CLI

`php -d xdebug.profiler_enable=On -d xdebug.profiler_output_dir=.`

### View output in Mac

```
brew install qcachegrind
brew install graphviz
```

Once you installed these, simply execute:

```
qcachegrind cachegrind.out.26620
```