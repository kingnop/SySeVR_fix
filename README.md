## Environments


### System

Ubuntu 18.04 (Tested)

### Step 1

- Joern 0.3.1
  - JDK 1.7
  - Neo4J 2.1.8 Community Edition
  - Gremlin for Neo4J 2.X
  - Apache Ant build tool
- Python 2.7

### Step 2

- Python 3.6
- Tensorflow 1.6
- Gensim 3.4

## Installation

### Joern 0.3.1

- #### **JDK 1.7**

  1. extract the tarball

     ```bash
     tar -xvf jdk-7u80-linux-x64.tar.gz -C /usr/loacl/java
     ```

  2. set environment variable

     > **/etc/profile**

     ```bash
     # Add These Content at the End of the File
     #######################################
     JAVA_HOME=/usr/local/java/jdk1.7.0_80
     JRE_HOME=/usr/local/java/jdk1.7.0_80
     PATH=$PATH:$JRE_HOME/bin:$JAVA_HOME/bin
     
     export JAVA_HOME
     export JRE_HOME
     export PATH
     #######################################
     
     update-alternatives --install "/usr/bin/java" "java" "/usr/local/java/jdk1.7.0_80/bin/java" 1
     
     update-alternatives --install "/usr/bin/javac" "javac" "/usr/local/java/jdk1.7.0_80/bin/javac" 1
     
     update-alternatives --install "/usr/bin/javaws" "javaws" "/usr/local/java/jdk1.7.0_80/bin/javaws" 1
     
     update-alternatives --set java /usr/local/java/jdk1.7.0_80/bin/java
     
     update-alternatives --set javac /usr/local/java/jdk1.7.0_80/bin/javac
     
     update-alternatives --set javaws /usr/local/java/jdk1.7.0_80/bin/javaws
     
     source /etc/profile
     ```

  3. verify

     ```bash
     java -version
     ```
     **You should receive a message which displays**

     ```bash
     java version "1.7.0_80"
     Java(TM) SE Runtime Environment (build 1.7.0_80-b15)
     Java HotSpot(TM) 64-Bit Server VM (build 24.80-b11, mixed mode)
     ```

- #### **Neo4j 2.1.8 Community Edition**

  1. extract the tarball

     ```bash
     unzip neo4j-community-2.1.8.zip
     mkdir -d /usr/local/neo4j
  mv /usr/local/neo4j ./Neo4j/neo4j-community-2.1.8/*
     ```

  2. modify configure files

     > **configure files are located in /usr/local/neo4j/conf**

     **neo4j-server.properties**

     ```bash
     # location of the database directory
     org.neo4j.server.database.location=/home/joern-0.3.1/.joernIndex/
     # Let the webserver only listen on the specified IP. Default is localhost (only
     # accept local connections). Uncomment to allow any connection. Please see the
     # security section in the neo4j manual before modifying this.
     org.neo4j.server.webserver.address=0.0.0.0
     ```

     **neo4j-wrapper.conf**

     ```bash
     # Java Heap Size: by default the Java heap size is dynamically
     # calculated based on available system resources.
     # Uncomment these lines to set specific initial and maximum
     # heap size in MB.
     wrapper.java.initmemory=512
     wrapper.java.maxmemory=10240 #as large as you can
     ```
     
  3. set environment variable
     
     > **/etc/profile**
     
     ```bash
     # Add These Content at the End of the File
     #######################################
     NEO4J_HOME=/usr/local/neo4j
     PATH=$PATH:$NEO4J_HOME/bin
     
     export NEO4J_HOME
     export PATH
     #######################################
     source /etc/profile
     ```
     
  4. start && verify
  
     ```bash
     /usr/local/neo4j/bin/neo4j console
     ```

- #### **Gremlin for Neo4J 2.X**

  > https://github.com/neo4j-contrib/gremlin-plugin

  ```bash
  unzip neo4j-gremlin-plugin-tp2-2.1.5-server-plugin.zip -d $NEO4J_HOME/plugins/gremlin-plugin
  ```

- #### **Apache Ant build tool**

  1. extract the tarball

     ```bash
     mkdir /usr/local/ant
     unzip -d /usr/local/ant apache-ant-1.8.4-bin.zip
     ```

  2. set environment variable

     > **/etc/profile**

     ```bash
     # Add These Content at the End of the File
     #######################################
     ANT_HOME=/usr/local/ant
     PATH=$PATH:$ANT_HOME/bin
     
     export ANT_HOME
     export PATH
     #######################################
     
     source /etc/profile
     ```

  3. verify

     ```bash
     ant -version
     ```

- #### **Joern 0.3.1**

  > https://joern.readthedocs.io/en/latest/installation.html#system-requirements-and-dependencies

  1. extract the tarball
     ```bash
  tar -xvf 0.3.1.tar.gz
     ```
     
2. extract the tarball of build dependencies
  
   ```bash
     cd joern-0.3.1
     tar -xvf lib.tar.gz
     ```
  
3. build the project
  
   ```bash
     cd joern-0.3.1
     ant
     ```
  
   **The executable JAR file is located in joern-0.3.1/bin/joern.jar**
  
4. set environment variable (optional)
  
   > **/etc/profile**
  
   ```bash
     # Add These Content at the End of the File
     #######################################
     JOERN_HOME=/home/joern-0.3.1/
     
     export JOERN_HOME
     #######################################
     ```
  
   > **~/.bashrc**
  
   ```bash
     # Add These Content at the End of the File
     #######################################
     alias joern='java -jar $JOERN/bin/joern.jar'
     #######################################
     ```
  
   ```bash
     source /etc/profile
     source ~/.bashrc
     ```
  
5. build additional tools (optional)
  
   ```
     cd joern-0.3.1
     ant tools
     ```
  
6. install python-joern
  
   ```bash
     apt install python-setuptools python-dev python-pip
     ```
  
   ```bash
     pip2 install py2neo==2.0 -i https://pypi.tuna.tsinghua.edu.cn/simple
     ```
  
   ```bash
     pip2 install py2neo-gremlin -i https://pypi.tuna.tsinghua.edu.cn/simple
     ```
  
   ```bash
     tar -xvf python-joern-0.3.1.tar.gz
     cd python-joern-0.3.1
     python2 setup.py install
     ```
  
7. install joern-tools
  
   ```bash
     pip2 install chardet -i https://pypi.tuna.tsinghua.edu.cn/simple
     pip2 install pygraphviz -i https://pypi.tuna.tsinghua.edu.cn/simple
     ```
  
   ```bash
     git clone https://github.com/fabsx00/joern-tools
     cd joern-tools
     python2 setup.py install
     ```
  
8. verify
  
   ```bash
     joern-lookup
     ```

## Using

### Step1 Generating Slices

> Work Dir: /home/SySeVR-master/Implementation/source2slice
>
> Code Dir: /home/code
>
> Recommended Memory Size: >=16GB (according to your code size)
>
> If you want to slice the NVD and SARD, you may divide them into parts.

1. install dependences

   ```bash
   apt install python-igraph
   ```

2. parse the source code

   >input: source codes
   >
   >output: .joernIndex

   ```bash
   rm -rf ./.joernIndex
   ```

   ```bash
   java -Xmx16g -jar $JOERN_HOME/bin/joern.jar /home/code
   ```

   This will create a neo4j database directory .joernIndex in this directory.

3. generate CFG

   >input: .joernIndex
   >
   >output: cfg_db

   ```bash
   # start neo4j at other terminal
   /usr/local/neo4j/bin/neo4j console
   ```

   ```bash
   mkdir cfg_db
   python2 get_cfg_relation.py
   ```

4. generate PDG

   >input: cfg_db .joernIndex
   >
   >output: pdg_db

   ```python
   # modify access_db_operate.py
   http.socket_timeout = 999999999 # a big number
   ```

   ```bash
   mkdir pdg_db
   python2 complete_PDG.py
   ```

5. generate call graph of functions

   >input: pdg_db .joernIndex
   >
   >output: dict_call2cfgNodeID_funcID

   ```bash
   mkdir dict_call2cfgNodeID_funcID
   python2 access_db_operate.py
   ```

6. generate four kinds of SyCVs

   >input: dict_call2cfgNodeID_funcID
   >
   >outout: arrayuse_slice_points.pkl, integeroverflow_slice_points_new.pkl, pointuse_slice_points.pkl, sensifun_slice_points.pkl

   ```python
   # modify points_get.py near the 128 rows
   # change "location" to ",location"
   for i in list_usenodes:
                   if str(i).find(",location")==-1:
                       list_usenodes.remove(i)
               loc_list=[]
               final_list=[]
               for i in list_usenodes:
                   #print(i)
                   if ',location' in str(i):
                       print(str(i))
                       location=str(i).split(",type:")[0].split(",location:")[1][1:-1].split(":")
                       count=int(location[0])
                       loc_list.append(count)
   
   ```

   ```bash
   python2 points_get.py
   ```

7. extract slices

   >input: dict_call2cfgNodeID_funcID, arrayuse_slice_points.pkl, integeroverflow_slice_points_new.pkl, pointuse_slice_points.pkl, sensifun_slice_points.pkl
   >
   >output: api_slices.txt, arrayuse_slice.txt, integeroverflow_slices.txt, pointeruse_slice.txt

   ```python
   # modify save-file-path in extract_df.py
   store_filepath = "integeroverflow_slices.txt"
   store_filepath = "arraysuse_slices.txt"
   store_filepath = "pointersuse_slices.txt"
   store_filepath = "api_slices.txt"
   ```

   ```python
   # add slice_op.py at 348 rows
   if not os.path.exists(path):
   	i += 1
   	continue
   ```

   **Due to the limit of memory, you may execute four functions in extract_df.py one by one.**

   ```bash
   python2 extract_df.py
   ```

8. get labels of slices

   >input: api_slices.txt, arrayuse_slice.txt, integeroverflow_slices.txt, pointeruse_slice.txt
   >
   >output: apt_slices_label.pkl, api_slices-vulline.pkl, array_slice_label.pkl, expr_slice_label.pkl, pointer_slice_label.pkl

   ```python
   # modify make_label.py at 70 rows
   # wrong format
   _dict_cwe2line = {}
   for _dict in dict:
   	for key in _dict.keys():
   		if _dict[key] not in _dict_cwe2line_target.keys():
   ```

   ```bash
   python2 make_label.py
   ```

9. combine labels with slices

   >input: apt_slices_label.pkl, api_slices-vulline.pkl, array_slice_label.pkl, expr_slice_label.pkl, pointer_slice_label.pkl, api_slices.txt, arrayuse_slice.txt, integeroverflow_slices.txt, pointeruse_slice.txt
   >
   >output: api_slices, arrayuse_slices.txt, integeroverflow_slices.txt, pointersuse_slices.txt

   ```bash
   mkdir slices label_source slice_label
   cp api_slices.txt arrayuse_slice.txt integeroverflow_slices.txt pointeruse_slice.txt ./slices
   cp apt_slices_label.pkl api_slices-vulline.pkl array_slice_label.pkl expr_slice_label.pkl pointer_slice_label.pkl ./label_source
   cd label_source
   mv expr_slice_label.pkl integeroverflow_slices.pkl
   mv apt_slices_label.pkl api_slices.pkl
   mv array_slice_label.pkl arrayuse_slice.pkl
   mv pointer_slice_label.pkl pointeruse_slice.pkl
   ```

   ```bash
   python2 data_preprocess.py
   ```

   

### Step2 Data Perprocess

pass

### Step3 Deep Learning

pass