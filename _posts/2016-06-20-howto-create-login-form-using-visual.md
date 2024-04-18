---
title: HowTo - Create Login Form Using Visual Basic 2010
date: '2016-06-20T21:10:00.000+07:00'
author: Arief JR
tags: [Visual Basic 2010, Login Form, Windows]
categories: [Programming]
---

Exactly i create software using visual basic has long time, because i don't want save for myself so i'll share for you if you need this tutorial **create login form using VB 2010.**  

### **Just Intermezzo!**

**[.... **Yep for a new learn programming, i think visual basic the first decent programming language you are trying so do i. Because i also like using windows but not often and for daily activity always using **Slackware Linux** **....]**

![](https://1.bp.blogspot.com/-4vQcjPC-gpY/V2bq-2HGo5I/AAAAAAAADaY/VK3cOdHYJr4TrucIKFKwNAYOjUupaQ6PACLcB/s1600/Visual%2BStudio%2B2010.PNG)

Next, before to visual basic you must create a database. You can use database from MySql, Access, or sqlite.  
But in this post, i'll create database from ms access.  

First create database from access, in here i'm using ms access 2010

![](https://2.bp.blogspot.com/-Lj8fowJ4cdo/V2bpa3ziPeI/AAAAAAAADZ0/-78QHgwSIegt4hWYKWiPhzALHjRI_m6KQCLcB/s1600/database%2Bcreate.png)

Easy steps for create database in ms access, after opened click to create database like above screenshot i named "rbdb" and right click in your database create table and choose to design view.  

In above screenshot, i create table akun a.k.a account then in colomn i fill Admin and password admin.

![](https://2.bp.blogspot.com/-gvvuGH0ocdQ/V2bs11VnylI/AAAAAAAADak/YJQfEh0ZVAQIw9WfantVyWV0p8Fr9-QcACLcB/s1600/database%2Bsave.png)

And after created, now save your database and don't forget visual studio could not read .accdb so save as to .mdb.  
For save as, click to save&publish in ms access, then save document as access 2000-2003 database then save.  

After saved, now open visualbasic. Then create form like this screenshot:

![](https://2.bp.blogspot.com/-sGcRD9kIhgA/V2bpfrvTtqI/AAAAAAAADaE/uJK79fFIOjwDZy0wrHSEh0TtS_VCG_KTACLcB/s1600/create%2Bform.png)

After created, now right click in solution explorer then add modules. Because if module does not exists, can't connected form to database.  
Here this module script for connect to database access:

_note: copy this script in to your module_  

```
Imports System.Data.OleDb
Imports System.IO
Imports vb = Microsoft.VisualBasic
Imports CrystalDecisions.CrystalReports.Engine
Imports CrystalDecisions.Shared

Module Module1

    Public conn As OleDbConnection
    Public da As OleDbDataAdapter
    Public ds As DataSet
    Public cmd As OleDbCommand
    Public rd As OleDbDataReader
    Public str As String
    Public name As String
    Public status As String
    Public name1 As String
    Public status1 As String

    Public cryRpt As New ReportDocument
    Public crtableLogoninfos As New TableLogOnInfos
    Public crtableLogoninfo As New TableLogOnInfo
    Public crConnectionInfo As New ConnectionInfo
    Public CrTables As Tables

    Public Sub Configure_module_report()
        With crConnectionInfo
            .ServerName = (Application.StartupPath.ToString & "\rbdb.mdb")
            .DatabaseName = (Application.StartupPath.ToString & "\rbdb.mdb")
            .UserID = ""
            .Password = ""
        End With

        CrTables = cryRpt.Database.Tables
        For Each CrTable In CrTables
            crtableLogoninfo = CrTable.LogOnInfo
            crtableLogoninfo.ConnectionInfo = crConnectionInfo
            CrTable.ApplyLogOnInfo(crtableLogoninfo)
        Next
    End Sub
    Public Sub connection()
        conn = New OleDbConnection("provider=microsoft.jet.oledb.4.0;data source=rbdb.mdb")
        Try
            If conn.State = ConnectionState.Closed Then
                conn.Open()

            End If
        Catch ex As Exception
            MsgBox("Failed connect to database", MsgBoxStyle.Critical, "Informastion")
            'Finally           
            'conn.Close()       
        End Try
    End Sub
End Module
```

After copy this script, then create a new connection using MS OleDb, click change to create new connection then select to Microsoft OleDb. Now select database name in this name _"rbdb"_.

![](https://3.bp.blogspot.com/-43rdoyeY49g/V2bphM6BRdI/AAAAAAAADaM/Gt9gS1XbWucd2sKb82RdcFEJwTuvMo5YQCLcB/s1600/add%2Bconnection.png)

Now go back to form 1, then double click form and copy paste this script:

```
Imports System.Data.OleDb
Imports System.IO
Public Class Form1
    Public status, name As String
    Dim CMD As New OleDbCommand
    Public Sub CmdLogin_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles CmdLogin.Click
        If TxtUser.Text = "" And TxtPwd.Text = "" Then
            MsgBox("Please Fill Username And Password", MsgBoxStyle.Information, "Info")
            Exit Sub
        Else
            Call connection()
            Dim login1 As String = "select * from akun where (user = '" & TxtUser.Text & "' and pass = '" & TxtPwd.Text & "')"
            CMD = New OleDbCommand(login1, conn)
            rd = CMD.ExecuteReader
            rd.Read()
            If rd.HasRows Then
                name = rd("Nama")
                status = rd("status")
                ProgressBar1.Increment(10)
                If ProgressBar1.Value = ProgressBar1.Maximum Then
                    Timer1.Stop()
                    ProgressBar1.Value = 0
                End If
                Me.Hide()
                Form2.Show()
            Else
                Timer1.Start()
                ProgressBar1.Increment(10)
                If ProgressBar1.Value = ProgressBar1.Maximum Then
                    Timer1.Stop()
                    ProgressBar1.Value = 0
                    MsgBox("Username or Password Wrong", MsgBoxStyle.Information)
                End If
            End If
        End If
    End Sub

    Public Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load
        TxtUser.MaxLength = 10
        TxtPwd.PasswordChar = ""
        TxtUser.Clear()
        TxtPwd.Clear()
    End Sub

    Private Sub CmdClose_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles CmdClose.Click
        Me.Close()
    End Sub

    Private Sub CheckBox1_CheckedChanged(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles CheckBox1.CheckedChanged
        If CheckBox1.Checked Then
            TxtPwd.UseSystemPasswordChar = False

        Else

            TxtPwd.UseSystemPasswordChar = True

        End If
    End Sub

    Private Function OdbcConnection() As String
        Throw New NotImplementedException
    End Function

    Private Sub Timer1_Tick(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Timer1.Tick
        If ProgressBar1.Value + 10 >= ProgressBar1.Maximum Then
            ProgressBar1.Value = ProgressBar1.Maximum
            Timer1.Stop()
        Else
            ProgressBar1.Value += 10
        End If
    End Sub
End Class
```

**Explanation module script**  

```
Public Sub Configure_module_report()
        With crConnectionInfo
            .ServerName = (Application.StartupPath.ToString & "\rbdb.mdb")
            .DatabaseName = (Application.StartupPath.ToString & "\rbdb.mdb")
            .UserID = ""
            .Password = ""
        End With

        CrTables = cryRpt.Database.Tables
        For Each CrTable In CrTables
            crtableLogoninfo = CrTable.LogOnInfo
            crtableLogoninfo.ConnectionInfo = crConnectionInfo
            CrTable.ApplyLogOnInfo(crtableLogoninfo)
        Next
    End Sub
```

This module script for create a report, so i discuss in here. This report will be use crystal report, and database access.  

```
Public Sub connection()
        conn = New OleDbConnection("provider=microsoft.jet.oledb.4.0;data source=rbdb.mdb")
        Try
            If conn.State = ConnectionState.Closed Then
                conn.Open()

            End If
        Catch ex As Exception
            MsgBox("Failed connect to database", MsgBoxStyle.Critical, "Informastion")
            'Finally           
            'conn.Close()       
        End Try
    End Sub
```

This module script for connect vb to database, if failed will show message box "failed connect to database" and `"provider=microsoft.jet.oledb.4.0;data source=rbdb.mdb"` to connect access database.  

**Explanation Form1 Script**  

```
Public Sub CmdLogin_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles CmdLogin.Click
        If TxtUser.Text = "" And TxtPwd.Text = "" Then
            MsgBox("Please Fill Username And Password", MsgBoxStyle.Information, "Info")
            Exit Sub
        Else
            Call connection()
            Dim login1 As String = "select * from akun where (user = '" & TxtUser.Text & "' and pass = '" & TxtPwd.Text & "')"
            CMD = New OleDbCommand(login1, conn)
            rd = CMD.ExecuteReader
            rd.Read()
```

This script for fill the password and user, if user and password match will executed and next can show to form2 or other form.

```
If rd.HasRows Then
                name = rd("Nama")
                status = rd("status")
                ProgressBar1.Increment(10)
                If ProgressBar1.Value = ProgressBar1.Maximum Then
                    Timer1.Stop()
                    ProgressBar1.Value = 0
                End If
                Me.Hide()
                Form2.Show()
            Else
                Timer1.Start()
                ProgressBar1.Increment(10)
                If ProgressBar1.Value = ProgressBar1.Maximum Then
                    Timer1.Stop()
                    ProgressBar1.Value = 0
                    MsgBox("Username or Password Wrong", MsgBoxStyle.Information)
                End If
            End If
```

This script for create access administration, if other user except admin cannot access to form which are desired besides the script i add progress bar if login progress bar will load like loading then if values in textbox not match will show message box username and password wrong.

```
Private Sub CheckBox1_CheckedChanged(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles CheckBox1.CheckedChanged
        If CheckBox1.Checked Then
            TxtPwd.UseSystemPasswordChar = False

        Else

            TxtPwd.UseSystemPasswordChar = True

        End If
    End Sub
```

This script for checked and unchecked for show password char, if you typo you can show this password with check on checkbox. See design in form 1.

```
Private Sub Timer1_Tick(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Timer1.Tick
        If ProgressBar1.Value + 10 >= ProgressBar1.Maximum Then
            ProgressBar1.Value = ProgressBar1.Maximum
            Timer1.Stop()
        Else
            ProgressBar1.Value += 10
        End If
    End Sub
```

This script tell: values for progress bar, loading until 10 second for opening form 2.  

I hope you not confused, if not understand can fill under comment in here and if i wrong give me suggestion.  

**Happy coding!**