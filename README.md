ethereum wallet recovery password multithread tool, baked from [pyethrecover](https://github.com/burjorjee/pyethrecover) and [pyethereum](https://github.com/ethereum/pyethereum), for using keystore v3 json file to help recover your lost password if you know some phrases using both brute and wordlist technique, start + end words, whole ascii or just numbers

[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://github.com/seevik2580/ethereum-wallet-recovery/graphs/commit-activity)
[![HitCount](http://hits.dwyl.com/seevik2580/ethereum-wallet-recovery.svg)](http://hits.dwyl.com/seevik2580/ethereum-wallet-recovery)

## Video demonstration
[https://www.youtube.com/watch?v=XVvLW26UPnY](https://www.youtube.com/watch?v=XVvLW26UPnY)

## requirements:
- Linux / Windows 10 Anniversary Update or newer and Windows Subsystem for Linux enabled.
- python 2.7.x
 
## dependency install:
- `sudo apt-get install libssl-dev build-essential automake pkg-config libtool libffi-dev libgmp-dev pandoc libreadline-dev zlib1g-dev curl git`

## install pyenv + python 2.7
```
curl https://pyenv.run | bash
echo 'export PATH="~/.pyenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)" ' >> ~/.bashrc
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
exec $SHELL
pyenv install 2.7.14
pyenv global 2.7.14
```

## python modules requirements:
```
pip install setuptools --upgrade
pip install joblib
pip install pypandoc
pip install markdown
pip install rlp==0.6.0
pip install py_ecc==1.1.3
pip install ethereum==2.1.5
```

## usage:

```
python generate.py    #wordlist generator
    -h                # help
    -w any,words      # comma separated words
    -i filename       # words from file separated by comma
    -a                # generate from ascii table
    -min number       # specify minimal generated word length
    -max number       # specify maximal generated word length
```

```
python recovery.py    #eth wallet password tester
    -h                # help
    -W file           # keystore ethereum wallet file
    -s file           # starting words separated by line
    -e file           # ending words separated by line
    -t N              # number of threads of jobs
    -w file           # wordlist file
    -b arg            # bruteforce type
      - ASCII         # whole ascii table
      - whatever char by char eg. 1234567890 or @#!$%^&*(
    -l N              # bruteforce character length
```

### uploaded test dummy wallet for test purposes, password:
# theAnswerToLifeUniverseAndEverythingIs42

### examples generate.py:
  #### makes all possible combinations of words separated by comma. 
  `python generate.py -w "fist,second,third"`      
  
  #### makes all possible combinations of words inside file input.txt separated by comma.
  `python generate.py -i input.txt`                
  
  #### makes all possible combinations of numbers 1,2,3,4,5,6,7,8,9,0 with minimal length 8. less length size is skipped.
  `python generate.py -min 8 -w "1,2,3,4,5,6,7,8,9,0"`

  #### makes all possible combinations of numbers 1,2,3,4,5,6,7,8,9,0 with maximal length 4, more length size is skipped.
  `python generate.py -max 4 -w "1,2,3,4,5,6,7,8,9,0"`

  - generated wordlist will be in same directory with name wordlist_01.txt. 
  - When wordlist reach maximum file size 50MB then new file will be created with next name wordlist_02.txt

### examples recovery.py:
  #### bruteforce numbers from 0 to 9 with size of 2
  `python recovery.py -W UTC--2017-07-12T00-06-42.772050600Z--f5751c906091b98be2a6be5ce42c573d704aedab -b 1234567890 -l 2`
  
  #### bruteforce @#! with size of 3
  `python recovery.py -W UTC--2017-07-12T00-06-42.772050600Z--f5751c906091b98be2a6be5ce42c573d704aedab -b @#! -l 3`
  
  #### bruteforce whole ASCII table with size of 4 
  `python recovery.py -W UTC--2017-07-12T00-06-42.772050600Z--f5751c906091b98be2a6be5ce42c573d704aedab -b ASCII -l 4`
  
  #### bruteforce numbers from 0 to 9 with size of 2 and starting words from file start.txt separated by lines
  `python recovery.py -W UTC--2017-07-12T00-06-42.772050600Z--f5751c906091b98be2a6be5ce42c573d704aedab -b 1234567890 -l 2 -s start.txt`
  
  #### bruteforce numbers from 0 to 9 with size of 2 and ending words from file end.txt separated by lines
  `python recovery.py -W UTC--2017-07-12T00-06-42.772050600Z--f5751c906091b98be2a6be5ce42c573d704aedab -b 1234567890 -l 2 -e end.txt`
  
  #### use words from wordlist generated by generate.py
  `python recovery.py -W UTC--2017-07-12T00-06-42.772050600Z--f5751c906091b98be2a6be5ce42c573d704aedab -w wordlist_01.txt`
  
  #### use starting words from file start.txt and words from wordlist generated by generate.py
  `python recovery.py -W UTC--2017-07-12T00-06-42.772050600Z--f5751c906091b98be2a6be5ce42c573d704aedab -s start.txt -w wordlist_01.txt`
  
  #### use words from wordlist generated by generate.py and ending words from file end.txt
  `python recovery.py -W UTC--2017-07-12T00-06-42.772050600Z--f5751c906091b98be2a6be5ce42c573d704aedab -w wordlist.txt -e end.txt`
  
  # donate 
  - ZEC t1ZFXmknFJEwYrbDm2jX5PZN8wHkQUDvDjD
  - BTC 1DkStuanmQLC9Xv4UgxbHRzhHqDwABkLfi
  
