kylin Mondrian

整合了一些适配kylin的方式，做了一些改动

1.Mondrian修改基于4.7.0.12分支源码<br>
2.在项目中增加了对kylin数据源的支持，参考了该开源项目kylin-mondrian-interaction
3.由于kylin的语法的UPPER函数只支持对表字段使用，而不支持对值使用，但mondrian会对值也加上upper函数，
  所以对kylin的方言做了一些改动，适配kylin的语法。
3.Mondrian初始只支持inner join，如果kylin的模型配置了left join，查询则会失败，参考开源项目mondrian-join-support做了修改。
  需要在cube节点下增加关联关系描述 如下:
          <Joins>
              <Join joinType='left' >
                  <JoinTable tableName='fhir_claim'>
                      <Column name='ENCOUNTER_ID' />
                  </JoinTable>
                  <JoinTable tableName='fhir_condition'>
                      <Column name='ENCOUNTER_ID' />
                  </JoinTable>
              </Join>
              <Join joinType='inner' >
                  <JoinTable tableName='fhir_claim'>
                      <Column name='CLAIM_DATE' />
                  </JoinTable>
                  <JoinTable tableName='fhir_date_dimension_v2'>
                      <Column name='DATE_KEY' />
                  </JoinTable>
              </Join>
          </Joins>


This is a source, binary or data distribution of Mondrian,
an OLAP Engine written in Java.

This code is released under the terms of the Eclipse Public
License v1.0 (EPL); see LICENSE.html.

For installation instructions, see doc/install.html
(http://mondrian.pentaho.com/documentation/installation.php).

The version is described in VERSION.txt.

Home page: http://mondrian.pentaho.com
Project home: http://sourceforge.net/projects/mondrian/
Email: jhyde@pentaho.com
