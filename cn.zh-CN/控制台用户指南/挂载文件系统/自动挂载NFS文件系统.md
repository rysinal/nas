# 自动挂载NFS文件系统 {#task_xmg_1kk_2fb .task}

本文档介绍如何修改Linux系统中的配置文件，使其重启时自动挂载NFS文件系统。

1.  已创建文件系统，详情请参见[创建文件系统](cn.zh-CN/控制台用户指南/管理文件系统.md#section_5jo_0kj_jn5)。
2.  已添加挂载点，详情请参见[添加挂载点](cn.zh-CN/控制台用户指南/管理挂载点.md#section_6xi_a3u_zkq)。
3.  已安装NFS客户端，详情请参见[安装NFS客户端](cn.zh-CN/控制台用户指南/挂载文件系统/手动挂载NFS文件系统.md#section_kvj_d02_szj)。

## 容量型/性能型NAS {#section_s5p_3m3_0zz .section}

您可以在Linux系统中配置 /etc/fstab 文件（推荐使用）或 /etc/rc.local 文件实现NFS文件系统自动挂载。

1.  登录[云服务器ECS](https://ecs.console.aliyun.com/)。
2.  配置自动挂载。 
    -   （推荐使用） 打开 /etc/fstab 配置文件，添加挂载命令。

        **说明：** 如果您是在CentOS6.x系统中配置自动挂载，您需先执行`chkconfig netfs on`命令，保证netfs开机自启动。

        -   如果您要挂载NFSv4文件系统，添加以下命令：

            ``` {#codeblock_xa1_fs1_x6w}
            file-system-id.region.nas.aliyuncs.com:/ /mnt nfs vers=4,minorversion=0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport 0 0
            ```

        -   如果您要挂载NFSv3文件系统，添加以下命令：

            ``` {#codeblock_35n_dl7_76g}
            file-system-id.region.nas.aliyuncs.com:/ /mnt nfs vers=3,nolock,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport 0 0
            ```

    -   打开/etc/rc.local配置文件，添加挂载命令。

        **说明：** 

        在配置/etc/rc.local文件前，请确保用户对/etc/rc.local和/etc/rc.d/rc.local文件有可执行权限。例如CentOS7.x系统，用户默认无可执行权限，需添加权限后才能配置/etc/rc.local文件。

        -   如果您要挂载NFSv4文件系统，添加以下命令：

            ``` {#codeblock_rwc_8h8_n9h}
            sudo mount -t nfs -o vers=4,minorversion=0,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport file-system-id.region.nas.aliyuncs.com:/ /mnt
            ```

        -   如果您要挂载 NFSv3 文件系统，添加以下命令：

            ``` {#codeblock_ghm_wat_r6b}
            sudo mount -t nfs -o vers=3,nolock,proto=tcp,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,_netdev,noresvport file-system-id.region.nas.aliyuncs.com:/ /mnt
            ```

        命令中各参数说明如下表所示。

        |参数|说明|
        |--|--|
        |挂载点| 挂载点包括挂载点域名和挂载点路径，请根据实际值替换。

        -   挂载点域名：添加挂载点时自动生成，无需手工配置。
        -   挂载点路径：挂载的目标地址，Linux 系统中的根目录（/）或任意子目录（如/mnt）。
 |
        |\_netdev|防止客户端在网络就绪之前开始挂载文件系统。|
        |0（noresvport 后第一项）|非零值表示文件系统应由 dump 备份。对于 NAS，此值为 0。|
        |0（noresvport 后第二项）|该值表示 fsck 在启动时检查文件系统的顺序。对于 NAS 文件系统，此值应为 0，表示 fsck 不应在启动时运行。|

        在挂载文件系统时，还可以选择多种挂载选项，这些选项使用逗号分隔列表的形式，具体选项与说明如下表所示：

        |选项|说明|
        |:-|:-|
        |rsize|定义数据块的大小，用于在您的客户端与云中的文件系统之间读取数据。建议值：1048576|
        |wsize|定义数据块的大小，用于在您的客户端与云中的文件系统之间写入数据。建议值：1048576|
        |hard|指定在NAS暂时不可用的情况下，使用文件系统上某个文件的本地应用程序时应停止并等待该文件系统恢复在线状态。建议启用该参数。|
        |timeo|指定时长（单位为 0.1 秒），即NFS客户端在重试向云中的文件系统发送请求之前等待响应的时间。建议值：600 分秒。|
        |retrans|指定NFS客户端应重试请求的次数。建议值：2|
        |noresvport|指定在网络重连时使用新的TCP端口，保障在网络发生故障恢复的时候不会中断连接。建议启用该参数。|

        **说明：** 配置参数时，应注意以下内容：

        -   如果您必须更改IO大小参数 （rsize和wsize），我们建议您尽可能使用最大值 （1048576），以避免性能下降。
        -   如果您必须更改超时参数 （timeo），我们建议您使用150或更大的值。该timeo参数的单位为分秒 （0.1 秒），因此150表示的时间为15秒。
        -   不建议使用soft选项，有数据一致性风险。如果您要使用soft选项，相关风险需由您自行承担。
        -   避免设置不同于默认值的任何其他挂载选项。如果更改读或写缓冲区大小或禁用属性缓存，会导致性能下降。
3.  执行`reboot`命令，重启云服务器 ECS。
4.  执行`mount -l`命令，查看挂载结果。 

    如果回显包含如下类似信息，说明挂载成功。

    ![挂载结果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21207/156896786051407_zh-CN.png)

    挂载成功后，您还可以通过`df -h`命令，可以查看文件系统的当前容量信息。如果挂载失败，请参见[挂载失败的排查与处理方法](../cn.zh-CN/控制台用户指南/挂载文件系统/挂载失败的排查与处理方法.md#)进行排查。

5.  挂载成功后，您可以在ECS上访问NAS文件系统，执行读取或写入操作。 

    您可以把NAS文件系统当作一个普通的目录来访问和使用，例子如下：

    ![读写操作](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18690/156896786054347_zh-CN.png)


## 极速型 NAS {#section_gsl_kkp_hhb .section}

您可以在 Linux 系统中配置 /etc/fstab 文件实现 NFS 文件系统自动挂载。

1.  登录[云服务器ECS](https://ecs.console.aliyun.com/)。
2.  打开 /etc/systemd/system/sockets.target.wants/rpcbind.socket 文件，注释掉IPv6相关的rpcbind参数，否则NFS的rpcbind服务自动启动会失败。 

    ``` {#codeblock_ytt_vbl_05p}
    vi /etc/systemd/system/sockets.target.wants/rpcbind.socket
    ```

    ![注释rpcbind参数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21506/156896786051186_zh-CN.png)

    **说明：** 如果您是在CentOS6.x系统中配置自动重启，您还需执行以下两个操作。

    1.  执行`chkconfig netfs on`命令，保证netfs开机自启动。
    2.  打开/etc/netconfig配置文件，注释掉inet6相关的内容。

        ![注释inet6相关内容](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21506/156896786051194_zh-CN.png)

3.  打开/etc/fstab配置文件，添加以下命令。 

    ``` {#codeblock_tj5_65v_w2c}
    file-system-id.region.extreme.nas.aliyuncs.com:/share /mnt nfs vers=3,nolock,proto=tcp,noresvport,_netdev 0 0
    ```

    命令中各参数说明如下表所示。

    |参数|说明|
    |--|--|
    |挂载点| 挂载点包括挂载点域名和挂载点路径，请根据实际值替换。

    -   挂载点域名：添加挂载点时自动生成，无需手工配置。
    -   挂载点路径：挂载的目标地址，Linux 系统中的根目录（/）或任意子目录（如/mnt）。
 |
    |vers|文件系统版本，目前只支持nfsv3。|
    |\_netdev|防止客户端在网络就绪之前开始挂载文件系统。|
    |0（noresvport 后第一项）|非零值表示文件系统应由 dump 备份。对于 NAS，此值为 0。|
    |0（noresvport 后第二项）|该值表示 fsck 在启动时检查文件系统的顺序。对于 NAS 文件系统，此值应为 0，表示 fsck 不应在启动时运行。|
    |挂载选项|详情请参见[容量型/性能型NAS](#section_s5p_3m3_0zz)的挂载选项说明表。|

4.  执行`reboot`命令，重启云服务器 ECS。
5.  执行`mount -l`命令，查看挂载结果。 

    如果回显包含如下类似信息，说明挂载成功。

    ![挂载结果](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21506/156896786051183_zh-CN.png)

    挂载成功后，您还可以通过`df -h`命令，可以查看文件系统的当前容量信息。如果挂载失败，请参见[挂载失败的排查与处理方法](../cn.zh-CN/控制台用户指南/挂载文件系统/挂载失败的排查与处理方法.md#)进行排查。

6.  挂载成功后，您可以在ECS上访问NAS文件系统，执行读取或写入操作。 

    您可以把NAS文件系统当作一个普通的目录来访问和使用，例子如下：

    ![读写操作](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18690/156896786054347_zh-CN.png)


## 常见错误排查 {#section_am0_b7e_vns .section}

如果挂载失败，请参见[挂载失败的排查与处理方法](../cn.zh-CN/控制台用户指南/挂载文件系统/挂载失败的排查与处理方法.md#)进行排查。

