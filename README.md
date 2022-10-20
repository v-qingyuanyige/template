## 项目配置

> 项目地址：git@github.com:v-qingyuanyige/template.git

- common
  - ***ResponseData***：定义统一返回数据的模板
  - ***ResponseDataUtil***：常见情况的统一返回数据预封装
  - ***ResultEnum***：自定义状态码与描述信息的枚举
- config
  - ***MybatisPlusConfig***：拦截器实现分页插件
  - ***ResponseControllerAdvice***：拦截器实现Controller层返回数据自动封装
  - ***SwaggerConfig***：Swagger配置

- utils
  - ***CodeGenerator***：自动生成后端代码

- templates
  - ***controller.java.vm***：Controller层代码模板

- ***application.yml***：配置文件

## MybatisPlus

### QueryWrapper

```java
    public List<DumpRecord> selectBySiteName(String site_name) {
        QueryWrapper<DumpRecord> wrapper = new QueryWrapper<>();
        wrapper.eq("site_name", site_name);
        return dumpRecordMapper.selectList(wrapper);
    }
```

### QueryWrapper+Page

```java
	public List<DumpRecord> conditionSelectAndPage(String site_name, 			String transporter, String start, String end, Integer 				pageNum, Integer pageSize) {
        Page<DumpRecord> page = new Page<>(pageNum, pageSize);
        QueryWrapper<DumpRecord> wrapper = new QueryWrapper<>();
        if(site_name != null)
            // site_name = site_name
            wrapper.eq("site_name", site_name);
        if(transporter != null)
            wrapper.eq("transporter", transporter);
        if(start != null && end != null)
            // exact_date between start and end
            wrapper.between("exact_date", start, end);
        return dumpRecordMapper.selectPage(page, wrapper).getRecords();
    }
```

