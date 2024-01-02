var 
 MyForm : TCLForm;
 MyMQTT : TclMQTT;
 BtnSend: TclProButton;
 LblDisplay: TclLabel;
 MemMsg: TclMemo;
 MsgList: TclMemo;
 msjBoxPanel, bigPanel : TclProPanel;
 clomosyImg : TclProImg;
 getMsjLayout : TclLayout;
 msj : String;

 procedure MemMsgEnter;
 begin
 getMsjLayout.Align:=alMostTop;
 end;

 Procedure MyMQTTStatusChanged;
 begin
   If MyMQTT.Connected Then 
   begin 
   LblDisplay.Text := 'Connected' ;
   LblDisplay.TextSettings.FontColor := clAlphaColor.clHexToColor('#0d7d0b');
   end
   Else 
   begin
   LblDisplay.Text := 'Not Connected';
   LblDisplay.TextSettings.FontColor := clAlphaColor.clHexToColor('#7a1209');

   end;
   //ShowMessage('MyMQTTStatusChanged');
 End;

 Procedure MyMQTTPublishReceived;
 begin
   msj := Clomosy.AppUserDisplayName;
   If MyMQTT.ReceivedAlright Then Begin

     MsgList.Lines.Add('                   ' + MyMQTT.ReceivedMessage);
   End;
 End;

 Procedure BtnSendClick;
 begin
  if Trim(MemMsg.Text) = '' then
    ShowMessage('Lütfen mesaj kısmını boş bırakmayınız.');
  else
  begin
   MyMQTT.Send(Clomosy.AppUserDisplayName+' : '+MemMsg.Text);
   MsgList.Lines.Add('You: '+MemMsg.Text);
   MemMsg.Text := '';
    getMsjLayout.Align:=alBottom;
    MsgList.setFocus;
  end;
 End;

begin
 MyForm := TCLForm.Create(Self);

 bigPanel:=MyForm.AddNewProPanel(MyForm,'bigPanel');
 clComponent.SetupComponent(bigPanel,'{"Align" : "Client","MarginBottom":10,"MarginTop":10,"MarginLeft":10,
"MarginRight":10,"RoundHeight":10,"RoundWidth":10,"BorderColor":"#5f00bf","BorderWidth":2}');

 LblDisplay:= MyForm.AddNewLabel(bigPanel,'LblDisplay','--');
 LblDisplay.Align := alTop;
 LblDisplay.Visible := True;
 LblDisplay.Margins.Left := 10;
 LblDisplay.StyledSettings := ssFamily;
 LblDisplay.TextSettings.Font.Size := 13;

 MyMQTT := MyForm.AddNewMQTTConnection(bigPanel,'MyMQTT');
MyForm.AddNewEvent(MyMQTT,tbeOnMQTTStatusChanged,'MyMQTTStatusChanged');
MyForm.AddNewEvent(MyMQTT,tbeOnMQTTPublishReceived,'MyMQTTPublishReceived');

 MyMQTT.Channel := 'chat';//project guid + channel
 MyMQTT.Connect;

 MsgList:= MyForm.AddNewMemo(bigPanel,'MsgList','');
 MsgList.Align := alClient;
 MsgList.Margins.Top := 10;
 MsgList.Margins.Bottom := 10;
 MsgList.Margins.Left := 10;
 MsgList.Margins.Right := 10;
 MsgList.TextSettings.WordWrap := True;
 MsgList.ReadOnly := True;

 getMsjLayout := MyForm.AddNewLayout(bigPanel,'getMsjLayout');
 getMsjLayout.Align:=alBottom;
 getMsjLayout.Height := 90;
 getMsjLayout.Margins.Bottom := 5;
 getMsjLayout.Width := 400;
 getMsjLayout.Margins.Left := 10;
 getMsjLayout.Margins.Right := 10;

 BtnSend := MyForm.AddNewProButton(getMsjLayout,'BtnSend','');
 clComponent.SetupComponent(BtnSend,'{"Align" : "Right" ,"MarginBottom":15,"Width" :80, "MarginTop" : 15,"MarginLeft" : 5,"Height":60,"BorderColor":"#ffffff"}');
 MyForm.SetImage(BtnSend,'https://clomosy.com/educa/send.png'); 
 MyForm.AddNewEvent(BtnSend,tbeOnClick,'BtnSendClick');

 msjBoxPanel:=MyForm.AddNewProPanel(getMsjLayout,'msjBoxPanel');
 clComponent.SetupComponent(msjBoxPanel,'{"Align" : "Left","RoundHeight":15,"Width" :240,"Height":30,
   "MarginLeft":10,"MarginBottom":20,"MarginTop":20,
   "RoundWidth":15,"BorderColor":"#bf00bf","BorderWidth":1}');

 MemMsg:= MyForm.AddNewMemo(msjBoxPanel,'MemMsg','');
 MemMsg.Align := alClient;
 MemMsg.Margins.Left := 5;
 MemMsg.Margins.Right := 5;
 MemMsg.Margins.Bottom := 5;
 MemMsg.Margins.Top := 5;
 MemMsg.TextSettings.WordWrap := True;
 MyForm.AddNewEvent(MemMsg,tbeOnEnter,'MemMsgEnter');

 MyForm.SetFormBGImage('https://clomosy.com/educa/bg2.png');
 MyForm.Run;
End;