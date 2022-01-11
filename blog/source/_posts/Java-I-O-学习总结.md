---
title: Java I/O 学习总结
date: 2020-12-1 17:56:24
tags:
---
## File.listFiles()源码分析

    public File[] listFiles() {
        String[] ss = list();
        if (ss == null) return null;
        int n = ss.length;
        File[] fs = new File[n];
        for (int i = 0; i < n; i++) {
            fs[i] = new File(ss[i], this);
        }
        return fs;
    }

    public String[] list() {
            SecurityManager security = System.getSecurityManager(); //获取系统安全接口
            if (security != null) {
                security.checkRead(path);
                //判断线程是否有读取文件的权限,权限可以自己去用System.setSecurityManager(SecurityManager  Object)去set
            }
            if (isInvalid()) {
                return null;
            }
            return fs.list(this);
        }

    final boolean isInvalid() {
            if (status == null) {
                status = (this.path.indexOf('\u0000') < 0) ? PathStatus.CHECKED
                                                           : PathStatus.INVALID;
            }
            return status == PathStatus.INVALID;
    }

    public void checkRead(String file) {
            checkPermission(new FilePermission(file,
                SecurityConstants.FILE_READ_ACTION));
    }

    public abstract String[] list(File f);

    @Override
    public native String[] list(File f);//调用的系统原生方法，要具体去看jdk的源码或者监控dll调用，
                                        // 反正只要明白此处使用的是操作系统原生的方法

checkRead
public void checkRead(String file)
如果不允许调用线程读取由字符串参数指定的文件，则抛出 SecurityException。
此方法用 FilePermission(file,"read") 权限调用 checkPermission。
如果重写此方法，那么通常应该在已重写方法将要抛出异常时调用 super.checkRead。
参数：
file - 取决于系统的文件名。
抛出：
SecurityException - 如果调用线程没有访问指定文件的权限。
NullPointerException - 如果 file 参数为 null。

