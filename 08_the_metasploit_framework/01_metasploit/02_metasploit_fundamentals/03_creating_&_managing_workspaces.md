# Creating & Managing Workspaces

+ Workspaces allow you to keep track of all your hosts, scans and activities and are extremely useful when conducting penetration tests as they allow you to sort and organize your data based on the target or organization.

**Note**: It is recommended to have separated workspaces for each engagement you participate at. You never want to mix data of one company with another.

+ MSFconsole provides you with the ability to create, manage and switch between multiple workspaces depending on your requirements.

+ We will be using workspaces to organize our assessments as we progress through the course.

**Note**: Remember you have to make sure the db is running in order to keep and load your workspaces.

## Practical demostration notes

Before beginning, check db status inside msfconsole by running `db_status`.

- The main command here is `workspace`. Run `workspace -h` to see all possible actions with this command.

- When listing workspaces with `workspace`, you can see which you are using because it is highlighted in red and with an * at the beginning. By default the msfconsole has the `default` workspace running.

**Note**: the MSFconsole actually tracks all of your data. For example, if you run `hosts` you will see all the hosts you have used in that workspace.

- In order to create/add a new workspace, just run `workspace -a $NAME`. By running `workspace` again we can see that the new workspace was created and it is currently selected. If we run `hosts` again, the workspace should be empty.

- To change between workspaces, we only need to run `workspace $NAME`.

- We can also rename workspaces by running `workspace -r $PREVIOUS_NAME $NEW_NAME`.

- To delete workspaces, we can run `workspace -d $NAME`.
