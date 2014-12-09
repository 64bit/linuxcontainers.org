# �ǿ��� API <!-- Current API -->
<!--
The current API is made of the following methods:
-->
�ǿ��� API �ϰʲ��Υ᥽�åɤǹ�������Ƥ��ޤ�:

### Ping (int junk) -> None
<!--
Ping is just used to test that the manager is alive and well, the value of the integer is ignored.
-->
Ping �� manager �������ư��Ƥ��뤫�ɤ�����ƥ��Ȥ���Τ˻Ȥ��ޤ���integer ���ͤ�̵�뤵��ޤ���

### GetPidCgroup (string controller, int pid) -> string cgroup
<!--
Takes a controller and PID and returns the cgroup path.
-->
controller �� PID ��Ϳ����ȡ�cgroup �Υѥ����֤��ޤ���

### GetPidCgroupAbs (string controller, int pid) -> string cgroup
<!--
Takes a controller and PID and returns the absolute cgroup path.
-->
controller �� PID ��Ϳ����ȡ�cgroup �����Хѥ����֤��ޤ���

### Create (string controller, string cgroup) -> int existed
<!--
Creates a new cgroup path in the provided controller, returns 1  
if the path already existed, 0 if it was created.
-->
���ꤷ�� controller ��˿����� cgroup �ѥ���������ޤ������˥ѥ���¸�ߤ������ 1 �򡢺����������������� 0 ���֤��ޤ���

### Chown (string controller, string cgroup, int uid, int gid) -> None
<!--
Chown the provided controller/cgroup path to the provied uid and gid,  
this will chown the directory as well as the cgroup.procs and tasks files.
-->
���ꤷ�� uid �� gid �ǡ����ꤷ���ѥ� controller/cgroup �� chown ���ޤ����ǥ��쥯�ȥꡢcgroup.procs��tasks �ե������ chown ���ޤ���

### Chmod (string controller, string cgroup, string file, int mode) -> None
<!--
Chmod the provided controller/cgroup/file path to the provided mode.
-->
���ꤷ���ѥ��� controller/cgroup/file ����ꤷ�� mode �� chmod ���ޤ���

### MovePid (string controller, string cgroup, int pid) -> None
<!--
Moves the provided PID into the provided controller/cgroup.
-->
���ꤷ�� PID ����ꤷ�� controller/cgroup �˰�ư���ޤ���

### MovePidAbs (string controller, string cgroup, int pid) -> None
<!--
Similar to MovePid but takes an absolute cgroup path rather than one relative  
to the caller (or proxy). This call is restricted to root as it lets you escape  
your current cgroup restrictions.
-->
MovePid ��Ʊ�ͤǤ������ƤӽФ��� (�⤷���ϥץ���) ��������� cgroup �ѥ��Ǥʤ������� cgroup �ѥ�����ꤷ�ޤ���
���θƤӽФ��ϸ��ߤ� cgroup �����¤򥨥������פ���Τ� root �����¤���Ƥ��ޤ���

### GetValue (string controller, string cgroup, string key) -> string value
<!--
Queries the value of the given key in the given controller/cgroup.  
The value is always returned as a string.
-->
���ꤷ�� controller/cgroup ��λ��ꤷ�� key ���ͤ��֤��ޤ������ʸ�����֤���ޤ���

### SetValue (string controller, string cgroup, string key, string value) -> None
<!--
Sets the value of the given key to that provided.
-->
���ꤷ�� contoller/cgroup ��λ��ꤷ�� key ���ͤ����ꤷ�ޤ���

### Remove (string controller, string cgroup, int recursive) -> int existed
<!--
Removes the provided cgroup, if recursive is set to 1, any sub-cgroup will also be removed.  
The return value indicates whether the cgroup existed.
-->
���ꤷ�� cgroup �������ޤ����⤷ recursive �� 1 �ξ��ϻ��ꤷ�� cgroup �Υ��� cgroup ��������ޤ���
�֤��ͤϻ��ꤷ�� cgroup ��¸�ߤ������ɤ����򼨤��ޤ���

### GetTasks (string controller, string cgroup) -> array of int
<!--
Returns an array of int representing all the PIDs in the provided cgroup path.
-->
���ꤷ�� cgroup �ѥ�������Ƥ� PID �� int ��������֤��ޤ���

### GetTasksRecursive (string controller, string cgroup) -> array of int
<!--
Returns an array of int representing all the PIDs in the provided cgroup path and its sub-directories.
-->
���ꤷ�� cgroup �ѥ��Ȥ��Υ��֥ǥ��쥯�ȥ� (��¹�� cgroup) ������Ƥ� PID �� int ��������֤��ޤ���

### ListChildren (string controller, string cgroup) -> array of string
<!--
Returns an array of string representing all the children (sub-cgroup) of the provided cgroup path.
-->
���ꤷ�� cgroup �ѥ������ƤλҶ� (���� cgroup) ��ʸ�����������֤��ޤ���

### RemoveOnEmpty (string controller, string cgroup) -> None
<!--
Marks the cgroup as removable when empty.  
Once the last task exists the cgroup, cgmanager will automatically remove it.
-->
���ꤷ�� cgroup �����ξ��˾õ��ǽ�ʥޡ�����Ĥ��ޤ���cgroup �κǸ�Υ��������ʤ��ʤä��Ȥ���cgmanager �ϼ�ưŪ�ˤ��� cgroup ��õ�ޤ���

### Prune (string controller, string cgroup) -> None
<!--
Calls RemoveOnEmpty on the cgroups path and any sub-directory (recursively).
-->
���ꤷ�� cgroup �ѥ��ȥ��֥ǥ��쥯�ȥ�� (�Ƶ�Ū��) RemoveOnEmpty ��ƤӽФ��ޤ���

<!--
Tasks will not be killed but once they all exit either naturally or  
because something killed them, the cgroup will disappear.
-->
�������� kill ����뤳�ȤϤ���ޤ��󤬡��������������� exit ���뤫��������ͳ�� kill ���줿�餹���� cgroup �Ͼä���Ǥ��礦��

### ListControllers () -> array of string
<!--
Returns an array of string representing the supported controllers.
-->
���ݡ��Ȥ���륳��ȥ����ʸ����Υꥹ�Ȥη������֤��ޤ���

### ListKeys (string controller, string cgroup) -> array of (string, uint, uint, uint)
<!--
Returns an array of (string name, uint uid, uint gid, uint mode) representing the available cgroup keys.
-->
���Ѳ�ǽ�� cgroup �Υ����� (string name, uint uid, uint gid, uint mode) �Υꥹ�Ȥ��֤��ޤ���

### api\_version (property) -> integer
<!--
The current internal API version, used for feature checks.
-->
���ߤ�����Ū�� API �ΥС��������֤��ޤ�������Ū�ʥ����å��˻Ȥ��ޤ���

# API ���������ɥ������ <!-- API definition document -->

<!--
The [org.linuxcontainers.cgmanager.xml file](https://github.com/cgmanager/cgmanager/blob/master/org.linuxcontainers.cgmanager.xml)
in the cgmanager cgmanager tree is used to generate the client library and is the authoritative API definition.
-->
cgmanager �ĥ꡼��� [org.linuxcontainers.cgmanager.xml �ե�����](https://github.com/cgmanager/cgmanager/blob/master/org.linuxcontainers.cgmanager.xml) �����饤����ȥ饤�֥�����������Τ˻Ȥ��ޤ��������ơ����Υե����뤬������ API ������Ǥ���