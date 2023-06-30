# Issues related to Python CLIs

### - `DirtyRepository: The repository is dirty. Please use the "git" command to clean it.`

Context: a renku/ omnibenchmark related command is run and returns an exit status with the above message.

Explanation: Renku (and Omnibenchmark) commands can only be run when there is no unsaved work.

Solution: run `renku_save()` (Python) or `renku save` (Bash) and rerun your command.

---

### Issues related to `omni_obj.update_object(all=True)`

Context: an error is raised when running the above command and no input data is imported. 

Explanation: there might be different reasons; the orchestrator is not set up, there is no input data,...

Solutions: depending on the problem, try the followings: 

- check that an orchestrator is set up for your Omnibenchmark: https://github.com/omnibenchmark/omni_essentials/blob/main/general/benchmark_categories.json

---

### - `omni_obj.update_result_dataset()` > `ParameterError: Invalid parameter value - These datasets don't exist:` OR `omni_obj.create_dataset()` > `Dataset zhengmix4eq-filterhvg-pinned already taken. Please use a different name.`

Context: Error or warning message when creating a dataset in an Omnibenchmark project

Explanation: the name is already taken or has conflicting dataset name. Typically, a subset of another name that our name matching algorithms could mix. Example: "dataset" vs "dataset-updated". 

Solution: change the `name:` in your `config.yml` to resolve the conflict; try to avoid spaces and `-` and rather use `_` and more descriptive names.

---

### - `GitError: Cannot commit changes`

Context: error when running a workflow. 

Explanation: It is possible that some files were generated in your `data` folder, where the output of your workflow will be moved. For reproducibility and tracing purpose, Renku doesn't allow files generation into your output `data` folder, if they were not generated by a Renku workflow. 

Solution: remove the problematic files from your `data` folder and run again your workflow command. 

---

### - `FileNotFoundError: [Errno 2] No such file or directory: '/opt/conda/lib/python3.9/site-packages/omniValidator/schemas/...'`

Explanation: you are using an older version of `omniValidator`. 

Solution: upgrade `omniValidator` to > 0.0.19