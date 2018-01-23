# maf_example

# Simple example for using MAF with Docker

## (Commands run on your local machine)

 1. Make a local directory where you will clone a repo with some MAF jupyter
    notebooks
    ```
    $ mkdir maf_results
    $ cd maf_results
    $ pwd
    /Users/myname/maf_results
    ```

 2. Clone the repository with the notebooks you would like to run into the
 newly created local directory `maf_results`.
  ```
  $ pwd
  /Users/myname/maf_results
  $ git clone https://github.com/lsst-pst/survey_strategy
  $ ls
  survey_strategy/
  ```

 3. Grab the data you would like to use with MAF if you do not already have it
 locally.
  ```
  $ wget http://astro-lsst-01.astro.washington.edu:8081/astro-lsst-01_2022.db
  $ ls
  astro-lsst-01_2022.db survey_strategy/

  ```
 4. Move the results database to the same directory as the notebooks.
  ```
  $ mv astro-lsst-01_2022.db /maf_demo_z/survey_strategy/db/.
  ```
 5. Start the Docker container (this single multi-line command). You can change
 `mycontainer` to whatever you would like the container name to be.

  ```
  docker run -it --rm --name mycontainer \
                     -v ${PWD}/survey_strategy:/home/docmaf/maf_local/survey_strategy \
                     -p 8888:8888 \
                     oboberg/maf:191017
  ```
  It may be useful to copy and paste this command into an executable shell script.


### After running step `5` you will be inside of the docker container in the shell window where you ran the command.
### Your command prompt should now look similar to this: ` [docmaf@2e6125b69fc5 ~]$`. In

## (Commands run in the container). Do not include the `[docmaf@2e6125b69fc5 ~]$` bit in the commands.

 1. Setup `sims_maf`
  ```
  [docmaf@2e6125b69fc5 ~]$ setup sims_maf -t sims
  ```

 2. Change to the notebook direcotry
  ```
  [docmaf@2e6125b69fc5 ~]$ cd maf_local/survey_strategy/db/
  ```

 3. Start a the jupyter notebook.
  ```
  [docmaf@2e6125b69fc5 db]$ jupyter notebook --ip=0.0.0.0 --no-browser
  ```
  After running command `3` you will see a message about copying and pasting a URL
  into a browser. Here is an example:
  ```
  Copy/paste this URL into your browser when you connect for the first time,
  to login with a token:
     http://0.0.0.0:8888/?token=sometoken
  ```
  Copy and paste the URL you were provided into your favorite
  local browser and use it like any other jupyter notebook.

  Any edits to the notebooks, as well as their outputs, will be saved to your local
  computer in the `~/maf_results/survey_strategy/db/` directory, or wherever you
  cloned the reop in step `1.`
