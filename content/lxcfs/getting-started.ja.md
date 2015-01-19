# git ����� lxcfs �Υӥ�ɤȼ¹� <!-- Building and running lxcfs from git -->

<!--
LXCFS is meant to be run once per host system at /var/lib/lxcfs.
-->
LXCFS �ϥۥ��ȥ����ƥऴ�Ȥ� 1 �Ĥ�����/var/lib/lxcfs �Ǽ¹Ԥ���褦�˺���Ƥ��ޤ���

<!--
Building lxcfs requires the following libraries and development headers:
-->
lxcfs ��ӥ�ɤ���ˤϰʲ��Υ饤�֥��ȳ�ȯ�إå���ɬ�פǤ�:

 - libcgmanager-dev
 - libnih-dbus-dev
 - libnih-dev
 - libfuse-dev

<!--
Then to build and run it from the git repository, do:
-->
�����ưʲ��Τ褦�� git ��ݥ��ȥ꤫�饳���ɤ���������ӥ�ɡ��¹Ԥ��ޤ���

    git clone git://github.com/lxc/lxcfs
    cd lxcfs
    ./bootstrap.sh
    ./configure
    make
    sudo mkdir -p /var/lib/lxcfs
    sudo ./lxcfs -s -f -o allow_other /var/lib/lxcfs/

<!--
And that's it, you'll have lxcfs mounted on top of /var/lib/lxcfs/.
-->
�ʾ�ǡ�/var/lib/lxcfs/ �� lxcfs ���ޥ���ȤǤ��ޤ���