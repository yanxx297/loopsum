# FuzzBALL with Loop Summarization

### Run CBs wtih FuzzBALL
```bash
cd cb-multios/tools/
./cb-test.py --directory ../../cb-multios/build/challenges/Palindrome --xml_dir \
../../cb-multios/build/challenges/Palindrome --concurrent 4 --timeout 5 \
--negotiate_seed --cb Palindrome --should_core
```
FuzzBALL output is stored in /tmp/fuzzball.log

### Test loop summarization
```bash
cd loopsum-fuzzball/examples/test-loopsum
../../exec_utils/fuzzball -use-loopsum -trace-loop -trace-iterations
 -trace-conditions -fuzz-start-addr [addr] -fuzz-end-addr 0x5006f63a
-solver smtlib -solver-path ../../../../lib/z3/build/z3 -linux-syscalls
-skip-call-ret-symbol [addr of atoi] -trace-stopping input-dependent -- ./input-dependent 0
# Add -trace-loop(-detailed) and -trace-loopsum(-detailed) for more information
```
