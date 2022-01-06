# SNIA-SSS-PTS

**ABSTRACT**

SNIA SSS PTS describes a solid state storage device-level performance test methodology, 
test suite and reporting format intended to provide an accurate, repeatable and reliable comparison 
of NAND Flash-based solid state storage products of various form factors, protocols and interfaces used in Client and Enterprise applications.

This is a software that can execute SNIA [Solid State Storage (SSS) Performance Test Specification (PTS)](https://www.snia.org/tech_activities/standards/curr_standards/pts) v2.0 test. It performs FIO testing through PHP CLI. Finally uses terminal to execute and generate report PDF.

Each directory is described as follows
  - **test**
  The main processes for testing PTS v2.0.
  - **temp**
  Store the temporary data during testings (set path by test/lib/parameter.json and create it by yourself)

#  
  **Environment**

  - **prerequisite**
  
    Ubuntu 20.04LTS SETUP install dependencies
    
        $sudo apt-get -y install fio gnuplot util-linux zip hdparm wkhtmltopdf xvfb git nvme-cli php-cli smartmontools
        
  - **support**

    Only one target at a time but with one or more test
    
    WARNING: If a device is specified (e.g. /dev/sdc), all data on that device will be erased during the course of testing.
        
#  
  **Usage**
  
  - **iops**
  
    IOPS Test - measures IOPS at a range of random block sizes and read/write mixes
  
        $sudo php run.php --verbose --target=/dev/sd<x> --test=iops --secureerase_pswd=pts --spec=<enterprise/client>
        $sudo php run.php --verbose --target=/dev/nvme<y> --test=iops --nvmeformat=1 --spec=<enterprise/client>
      
  - **throughput**
  
    Throughput Test - measures sequential read and write throughput (MB/s) in steady state
    
        sudo php run.php --verbose --target=/dev/sd<x> --test=latency --secureerase_pswd=pts --spec=<enterprise/client>
        sudo php run.php --verbose --target=/dev/nvme<y> --test=latency --nvmeformat=1 --spec=<enterprise/client>
  
  - **latency**
  
    Latency Test - measures IO response times for 3 block sizes (0.5k, 4k and 8k), and 3 read/write mixes (100/0, 65/35 and 0/100). 
    
        sudo php run.php --verbose --target=/dev/sd<x> --test=throughput --secureerase_pswd=pts --spec=<enterprise/client>
        sudo php run.php --verbose --target=/dev/nvme<y> --test=throughput --nvmeformat=1 --spec=<enterprise/client>
        
  - **wsat**
  
    Write Saturation Test - measures how drives respond to continuous 4k random writes over time and total GB written (TGBW). 
    
        sudo php run.php --verbose --target=/dev/sd<x> --test=wsat --wsat_wl=0 --wsat_time=6 --secureerase_pswd=pts --spec=<enterprise/client>
        sudo php run.php --verbose --target=/dev/nvme<y> --test=wsat --wsat_wl=0 --wsat_time=6 --nvmeformat=1 --spec=<enterprise/client>
    
  _Enterprise_: \
  Servers in data centers, storage arrays, and enterprise wide / multiple user environments that employ direct attached storage, 
  storage attached networks and tiered storage architectures. \
  _Client_: \
  laptop or desktop computers used in small office, home, mobile, entertainment and other single user applications.

#
  **Report**
  
  test saves results under test/lib directory
  
  - perform IOPS test against device Transcend SSD452K2 1T
  
  <img src="https://github.com/transcend-information/SNIA-SSS-PTS/blob/main/imgs/1641261538248.jpg" width=95% height=95%>
  
#  
  **Note**
This software contains code derived from [cloudharmony/block-storage](https://github.com/cloudharmony/block-storage) and [Alan-ADATA/SSS-PTS-TEST](https://github.com/Alan-ADATA/SSS-PTS-TEST).
