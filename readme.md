# ChatGPT for Delphi

#### By Bruno Fierens

#### Access the ChatGPT REST API from a Delphi or maXbox app

## Technologies Used

* Delphi VCL or FMX / Lazarus
* TMS FNC Core
* Delphi JSON
* WinHttp.WinHttpRequest.5.1

### Creating the client with TRestClient in maXbox4
```delphi
function TRestResource3_AskChatGPT(askstream: string; 
                                 aResponseHeader:TRestResponseHandler):string;
var pstrm: TStream;
    JPostdat: string;
    jo: TJSON; arest: TRestResource;
begin
  JPostDat:= '{'+
    '"model": "text-davinci-003",'+
    '"prompt": "%s",'+
    '"max_tokens": 2048,'+
    '"temperature": 0.15}';

  with TRestClient.create(self) do begin
      arest:= Resource('https://api.openai.com/v1/completions');
      arest.ContentType('application/json');
      arest.Authorization('Bearer '+CHATGPT_APIKEY2);
      ConnectionType:= hctWinInet;
    try
      pstrm:= TStringStream.create(format(JPostDat,[askstream]));
      jo:= TJSON.Create(); 
      jo.parse(arest.Post(pstrm)); 
      writeln('responsecode: '+itoa(responsecode)+' verifycert: '+botostr(verifycert));
      result:= jo.values['choices'].asarray[0].asobject['text'].asstring;
    finally
      Free;
      jo.Free;
      pStrm.Free;        
    end; 
  end; //with   
end; 
```
## Package Diagram

![TRestClient_pac2](https://user-images.githubusercontent.com/109789632/230425938-274da234-e225-4be1-8689-5bbac881ff20.png)


## Description

This is a simple demo of how to use the ChatGPT API from a Delphi or Lazarus app from any framework or any platform. Get the ChatGPT API key for your own use and add it to APIKEY.inc

## Setup/Installation Requirements

* Delphi 10.2 or newer
* TMS FNC Core from https://www.tmssoftware.com/site/tmsfnccore.asp
* Get the ChatGPT API key from https://beta.openai.com/account/api-keys 

![1202_chatgpt_maxboxscript](https://user-images.githubusercontent.com/109789632/228959260-861d3a0f-1d9e-42a5-85c7-bf0cc2111c89.png)

## Known Bugs

* No issues reported 

## License

MIT

Copyright (c) Dec 2022 by Bruno Fierens tmssoftware.com 
