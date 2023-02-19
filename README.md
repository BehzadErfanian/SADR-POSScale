# SADR-POSScale
This file for communicate with POS Scale device made by "Tozin SADR"

Add SadrPosScale.DLL to your Projects. This DLL made with .Net Framework 2.0

## Step 1:
Create an object of DLL and events then Connect to Scale:

        public PosScaleDevice PosScale = null;
        public void Connect()
        {
            try
            {
                PosScale = new PosScaleDevice(PortNames.Text, 9600);
                PosScale.ConnectToScale();
                PosScale.DeviceConnected += MainForm_DeviceConnected;
                PosScale.DeviceDisconnected += MainForm_DeviceDisconnect;
                PosScale.ResultEvent += MainForm_ResultEvent;
                PosScale.WeightEvent += MainForm_WeightEvent;
                PosScale.SendCommandConfirm += MainForm_SendCommandConfirm;
            }
            catch { }
        }
        
## Step 2:
Create Events:

        private void MainForm_SendCommandConfirm(object sender, EventArgs e)
        {
           //This event rais when send and set command to scale be OK
        }

        private void MainForm_WeightEvent(object sender, WeightEventArgs e)
        {
           //This event rais every 300 miliseconds and have current weight of scale
           // Current weight show in ==> e.Weight
           // Value is 5 digit numbers that shown weight with grams unit
           // For example: 01000 for 1Kg or 1000 gram
           // For negetive weight shown -1000 for -1Kg
        }

        private void MainForm_ResultEvent(object sender, ResultEventArgs e)
        {
          //This event rais send and set command or resulation to scale is not OK
          //This event shown error in string to this parameter ==> e.Result
        }

        private void MainForm_DeviceDisconnect(object sender, EventArgs e)
        {
          //This event rais when scale is disconnected
        }

        private void MainForm_DeviceConnected(object sender, EventArgs e)
        {
          //This event rais when scale is connected
        }

## Step 3:
Other Methods:

### Manual Disconect frome scale

PosScale.DisconnectFromScale();

### Tare Weight

PosScale.SendKey(KeyType.Tare);

this method set weight to Zero "00000"
