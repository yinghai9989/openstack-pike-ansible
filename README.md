# Install openstack pike use ansible 2.4 on ubuntu 16.04.3 with openvswitch 2.8
# openstack pike ansible


使用ansible 2.4.2.0 在ubunut 16.04.3 64位系统上安装 openstack pike ，其中neutron网络使用openvswitch 2.8.0

注1：此版本为在线安装版本，安装过程中需要下载依赖包及相应的软件包 如果安装过程缓慢或者不成功请挂代理

注2：此版本支持自定义所有主机名、openstack组件密码，自动修改主机hosts


部署拓扑 ：
![image](https://github.com/yinghai9989/openstack-pike-ansible/blob/master/topo.png)
   
相关节点安装的组件请见拓扑示意。

注：swift和cinder节点可以安装在计算节点上。
   此时建议计算节点上部署3块硬件。即 cinder安装在comput1，compute2 上swift存储节点安装在compute3，copmute4上。

部署步骤：

  【ansible安装】---【关联ssh秘钥】---【配置变量】---【开始安装openstack pike】

1、【ansible安装】

   请参照ansible官方文档
 
2、【关联ssh秘钥】

   ssh-keygen
 
   ssh-copy-id root@controller 
 
   ...
 
3、【配置变量】
 
   编辑hosts： 根据部署规划填写主机ip
 
   编辑group_vars/all： 根据实际情况填写
 
4、【开始安装openstack pike】
   请根据实际需要安装模块
  控制节点上的模块
   - barbican
   - tacker
   - networking-sfc
   - mistral
   - ceilometer  #There are problems with installation
   计算节点上的模块
   - networking-sfc-compute
   - ceilometer-compute   #There are problems with installation
   目前还有些问题在调试。

   执行 bash cmd_deploy 
   注在安装之前请检查一下所有节点的时间和时区是否一致，如不一致请注意
   ansible all -m shell -a timedatectl
  
 5、【FAQ】
 
 5.1、脚本可以分步安装
 
      ansible-playbook -i hosts deploy_pike.yml --tags=sshauth
      
      ansible-playbook -i hosts deploy_pike.yml --tags=common
      
      ...
   
5.2、其他问题

   如有其他问题请联系:chen1893@163.com 或者chen1893@gmail.com
