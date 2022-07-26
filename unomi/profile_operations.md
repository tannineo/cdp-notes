# Operations on Profiles

## Merge Profiles

Solution - extend the default action:

https://github.com/apache/unomi/blob/master/plugins/baseplugin/src/main/java/org/apache/unomi/plugins/baseplugin/actions/MergeProfilesOnPropertyAction.java

## Import/Export Profiles

Unomi RESTful API 提供了 Profile 的导入导出: https://unomi.apache.org/manual/latest/#_profile_import_export

能够配置 csv 的 column mapping.
