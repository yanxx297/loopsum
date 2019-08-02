# Loop Summarization
Implement loop summarization <sup>[1](#footnote1)</sup> on FuzzBALL and evaluate it with CGC benchmark.

### Test loop summarization with toy examples
There are several examples in ``examples/loopsum``, run them with the following cmdline to test.
You can add ``-trace-loop(-detailed)`` and ``-trace-loopsum(-detailed)`` for more debugging information.
```bash
cd fuzzball-loopsum/examples/loopsum
../../exec_utils/fuzzball -use-loopsum -trace-loop -trace-iterations -trace-conditions \
 -fuzz-start-addr [addr] -fuzz-end-addr 0x5006f63a -solver smtlib \
 -solver-path ../../../../lib/z3/build/z3 -linux-syscalls \
-skip-call-ret-symbol [addr of atoi] -trace-stopping input-dependent -- ./input-dependent 0
```

### Run CBs wtih (loopsum)FuzzBALL
Use the cmdline bellow to run [Palindrome](https://github.com/yanxx297/cb-multios/tree/master/challenges/Palindrome) on FuzzBALL.
pyelftools is required by this script.
```bash
cd cb-multios/tools/
./cb-test.py --directory ../../cb-multios/build/challenges/Palindrome --xml_dir \
../../cb-multios/build/challenges/Palindrome --concurrent 4 --timeout 5 \
--negotiate_seed --cb Palindrome --should_core
```
Results are logged in [this google spreadsheet](https://docs.google.com/spreadsheets/d/1ZJjkgshZrRyk-zBE38rshinlcJrFB_bD-qv12G8EW1A/edit#gid=0).

FuzzBALL output is stored in outputs/CB_name for debugging purpose.

### Compile SV-COMP benchmark
```bash
cd sv-benchmarks/c
make SYNTAX_ONLY=0 CC=clang
```
NOTE: Some programs only compiled with gcc, some only clang, switch to the other when get stuck.   
Binaries are in``/c/bins``.

## Reference
<a name="footnote1">[1]</a>
Patrice Godefroid and Daniel Luchaup. Automatic partial loop summarization in
dynamic test generation. In Proceedings of the 2011 International Symposium on
Software Testing and Analysis, ISSTA ’11, pages 23–33, New York, NY, USA, 2011.
ACM.