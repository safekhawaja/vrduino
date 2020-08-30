void Start () {
      UduinoManager.Instance.OnDataReceived += ReadIMU;
    }
    
     public void ReadIMU (string data, UduinoDevice device) {
        //Debug.Log(data);
        string[] values = data.Split('/');
        if (values.Length == 5 && values[0] == imuName) // Rotation of the first one 
        {
            float w = float.Parse(values[1]);
            float x = float.Parse(values[2]);
            float y = float.Parse(values[3]);
            float z = float.Parse(values[4]);
            this.transform.localRotation = Quaternion.Lerp(this.transform.localRotation,  new Quaternion(w, y, x, z), Time.deltaTime * speedFactor);
        } else if (values.Length != 5)
        {
            Debug.LogWarning(data);
        }
        this.transform.parent.transform.eulerAngles = rotationOffset;
      //  Log.Debug("The new rotation is : " + transform.Find("IMU_Object").eulerAngles);
    }
    
public bool setOrigin = false;
Quaternion rotOffset = Quaternion.identity;

void Update()
    {
        if(setOrigin)
        {
            rotOffset = this.transform.rotation;
            setOrigin = false;
        }
    }

void ReadIMU (string data, UduinoDevice device) {
    //...
    this.transform.rotation = new Quaternion(w, x, y, z) * Quaternion.Inverse(rotOffset);
   }
