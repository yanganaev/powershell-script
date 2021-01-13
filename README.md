# Создание скрипта, создающего виртуальные машины
Выполните следующие действия в Cloud Shell справа, чтобы создать скрипт.

1. Переключитесь в Cloud Shell в домашнюю папку.
 `cd $HOME\clouddrive`

2. Создайте текстовый файл с именем ConferenceDailyReset.ps1.
`touch "./ConferenceDailyReset.ps1"`

3. Откройте интегрированной редактор и выберите файл ConferenceDailyReset.ps1.
`code "./ConferenceDailyReset.ps1"`

4. Для начала сохраните входной параметр в переменной. Добавьте следующую строку в скрипт:
`param([string]$resourceGroup)`

# Примечание:
# В обычной системе нужно еще пройти аутентификацию в Azure, указав учетные данные в Connect-AzAccount, и вы можете сделать это в скрипте. Но в среде Cloud Shell в этом нет необходимости, ведь вы уже прошли аутентификацию.

5. Запросите имя пользователя и пароль для учетной записи администратора виртуальной машины и сохраните результат в переменной:
`$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."`

6. Создайте цикл, который выполняется три раза:
```console
For ($i = 1; $i -le 3; $i++)
{

}
```
7. В теле этого цикла создайте имя для каждой виртуальной машины, сохраните его в переменной и выведите на консоль:
```console
$vmName = "ConferenceDemo" + $i
Write-Host "Creating VM: " $vmName
```

8. Создайте виртуальную машину с помощью переменной $vmName:
`New-AzVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Image UbuntuLTS`

9. Сохраните файл. Можно использовать меню "..." в правом верхнем углу редактора. Также поддерживаются распространенные сочетания клавиш для сохранения.

# Готовый сценарий будет выглядеть так:
```console
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i
    Write-Host "Creating VM: " $vmName
    New-AzVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Image UbuntuLTS
}
```


Выполнение скрипта
Закройте редактор через контекстное меню "...".
Выполните скрипт.
`.\ConferenceDailyReset.ps1 learn-7744591b-6aa0-4c0d-86db-10ecd522a3ad`

Выполнение скрипта может занять несколько минут. Когда он завершится, проверьте созданные ресурсы в указанной группе ресурсов, чтобы убедиться в успешности выполнения:

`Get-AzResource -ResourceType Microsoft.Compute/virtualMachines`

Вы должны увидеть три виртуальные машины с уникальными именами.

Вы написали сценарий, автоматизирующий создание трех виртуальных машин в группе ресурсов, указанной параметром сценария. Это короткий и простой сценарий, но он автоматизирует процесс, который может занять много времени при работе вручную на портале.
