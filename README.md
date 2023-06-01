# JeMoVeClLi

Jenkins+Molecule+Vector+Clickhouse+Lighthuse


Примечание:


1.Jenkins
Файл ` DeclarativeJenkinsfile ` для Declarative pipeline  
Файл `Jenkinsfile` для Multibranch pipeline (репозиторий содержит две ветки: main и second - с разными версиями Jenkinsfile и converge.yml)  
Файл `ScriptedJenkinsfile` для простого Scripted pipeline тестировании ролей в Molecule  
Файл `ScriptedJeMoVeClLiJenkinsfile` для Scripted pipeline автоматизации создания машинок в Яндекс.Облаке и разворачивании на них всего JeMoVeClLi стека  
Файл `playbooks/demo.yml` - Ansible playbook для разворачивания JeMoVeClLi стека. Требует inventory файл. Используется в скрипте автоматизации ScriptedJeMoVeClLiJenkinsfile  

2. Испытывался только на CentOS 7  

3. Создаются три контейнера:  

`clickhouse` с открытыми портами 9000 и 8123 для возможности ручной проверки через GUI vector  
`lighthouse` с открытым портом 8080 для возможности ручного контроля  
  
`cleanup.yml` - playbook Molecule для этапа Cleanup - предназначен для чистки сервисов от следов проверок, а именно обнуляется таблица в Clickhouse и удаляются контролируемые Vector файлы  
`converge` - playbook Molecule для этапа Converge - подготовка инфраструктуры сервисов: устанавливает скрипт эмулятор SystemD во все контейнеры и применяет все роли к соответствующим контейнерам  
`molecule` - конфигурационный файл Molecule  
`requirements` - файл зависимостей Molecule для Ansible-galaxy  
`verify` - основной playbook Molecule для этапа verify - верифицирует установку Vector и Lighthouse, создаёт контролируемые Vector файлы и наполняет их содержимым  
`verify_clickhouse` - playbook запрашивает данные из Clickhouse и сравнивает их с эталоном. Реализован отдельно с поддержкой нескольких итераций, так как из-за особенностей реализации Vector не все данные сразу отправляются в Clickhouse.  
  

