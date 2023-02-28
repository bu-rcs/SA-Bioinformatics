# The SCC
The Shared Computing Cluster or [SCC](http://www.bu.edu/tech/support/research/system-usage/scc-quickstart/) is an amazing resource that gives you access to remote computers with tons of computing power, memory, and storage. It is also an ideal environment to store data, especially data that you anticipate sharing with BU-collaborators. Accessing the SCC requires being a member of a `project`, which is typically managed by your PI. You can reach out the RCS about the SCC at help@scc.bu.edu if you are having trouble.

# OnDemand
For most purposes, the most convenient way to access the SCC is through the [OnDemand](https://scc-ondemand.bu.edu/) page. From here you can navigate the tabs at the top of the page:
* `Files`: an interactive file browser
* `Quota`: disc usage quota on your `projects`
* `Login Nodes`: Terminal sessions into login nodes
* `Interactive Apps`: Run apps like Spyder, R Studio, and Jupyter on the SCC with direct access to files on the SCC

You can learn more about OnDemand at BU from [TechWeb](http://www.bu.edu/tech/support/research/system-usage/scc-ondemand/)

# R setup
By default R installs packages to your home directory, which on the SCC has limited disc space. To avoid running out of disc space in your home directory, you can use the following code to point R to install packages in a specified directory:

```bash
echo "R_LIBS_USER=/path/to/directory/" >> ~/.Renvrion
```

You can read more about this here: https://stackoverflow.com/questions/15170399/change-r-default-library-path-using-libpaths-in-rprofile-site-fails-to-work

# Conda setup (for Python users)
[Conda](https://docs.conda.io/en/latest/) is a package manager (mainly) for Python. It allows you to install packages with automatic dependency/conflict checking and allows you to create separate "environments" with different sets of packages installed. Documentation for using conda on the SCC can be found here: https://www.bu.edu/tech/support/research/software-and-programming/common-languages/python/anaconda/.

Before installing packages with conda on the SCC though, you will want to configure conda to save packages in a directory other than your home directory, since your home directory has limited space. Instructions to do so are [here](https://www.bu.edu/tech/support/research/software-and-programming/common-languages/python/anaconda/#config) and are reproduced here:

For the following commmand, update `your_project` to the name of the SCC project you belong to and `your_name` to your user name (or whatever the name of your working directory within your project is). For example, if my working directory is `/projectnb/awesome_lab/michael/`, I would set `your_project=awesome_lab` and `your_name=michael`. After you have update the variable values paste this into a SCC terminal and hit enter.
```bash
your_project=project_name_here
your_name=your_name_here

echo -e "envs_dirs:
    - /projectnb/$your_project/$your_name/.conda/envs
    - ~/.conda/envs
pkgs_dirs:
    - /projectnb/$your_project/$your_name/.conda/pkgs
    - ~/.conda/pkgs
env_prompt: ({name})" > ~/.condarc
```

After you have configured your conda package installation directory, you can create a new conda environment:
```bash
module load miniconda
conda create --name myenv
```
Where `myenv` is whatever name you want to give your environment (like your username). Note that this new environment will be crated in the directory you specified in the `.condarc` file above.

While it is not recommended, conda can be loaded upon logging into the SCC, by adding the module load command to your `~.bashrc` file with this command: `echo "module load miniconda" >> ~.bashrc`. 

When installing a package using pip, be user to specify the `--user` flag: `pip install --user <package>`

# Packages installed on the SCC
The SCC has many packages already available, a list of which can be seen here: http://sccsvc.bu.edu/software/#/ (you can subset to `Bioinformatics`) or with the `module avail`. You can use `module avail <package name>` to check for a specific package. If you don't see a package you need, you can request it here: http://www.bu.edu/tech/support/research/software-and-programming/software-and-applications/request-software/.

To use a package, you can load it with `module load <package name>`. All modules can be unloaded with `module purge`.

# Batch jobs
A huge convenience of the SCC is the ability to submit jobs that will run on worker nodes and return the results when the job is finished. [Here](https://github.com/Boston-University-Microbiome-Initiative/BUfqdump/blob/master/fqdump.qsub) is an example of a script that downloads fastq files from NCBI. Documentation on how to submit batch jobs on the SCC can be found here: http://www.bu.edu/tech/support/research/system-usage/running-jobs/submitting-jobs/. 

# Local Access
As an alternative to OnDemand can also access the SCC by ssh-ing. Open a ssh-able terminal session with Terminal on Mac or Windows Powershell on Windows and enter `ssh <BU username>@scc1.bu.edu` and then enter your password.

TO DO:
* Graphics forwarding

