EventRouter is a class for broadcasting messages to subscribers.  Clients of the EventRouter register themselves by calling Subscribe and passing in the even they are interested in along with a delegate to be called back when the event is received.  Events are published via the Publish method which allows arbitrary data to be passed along with the event to be interpreted by the event receiver.  Events do not have to be pre-defined.

Publish and Subscribe methods also have an optional id parameter which will filter the events a receiver gets to just those that match the provided event and id.  Subscribing to an event with no id will result in receiving all events of the specified type.

Example of a simple publish and subscribe class, not using any id filtering.
----------------------------------------------------------------------------

### Sender.cs
```C#
public enum SenderEvent {
	Test
}

public class Sender {
	public void Send() {
		EventRouter.Publish(SenderEvent.Test, this, "Hello World");
	}
}
```

### Receiver.cs
```C#
public class Receiver {
	public Receiver() {
		EventRouter.Subscribe(SenderEvent.Test, OnSenderEvent);
	}

	void OnSenderEvent(EventRouter.Event evt) {
		if(evt.HasData) {
			Console.WriteLine("Received event: " + evt.Type + " from: " + evt.Sender.ToString() + " with data: " + evt.Data[0]);
		}
		else {
			Console.WriteLine("Received event: " + evt.Type + " from: " + evt.Sender.ToString() + " with no data");
		}
	}
}
```

Example of a publish and subscribe using id's to filter specific messages.
--------------------------------------------------------------------------

### Sender.cs
```C#
public enum SenderEvent {
	Test
}

public class Sender {
	public void SendA() {
		EventRouter.Publish("A", SenderEvent.Test, this, "Hello World");
	}
	
	public void SendB() {
		EventRouter.Publish("B", SenderEvent.Test, this, "Hello World");
	}
}
```

### Receiver.cs
```C#		
public class Receiver {
	public Receiver() {
		EventRouter.Subscribe("A", SenderEvent.Test, OnSenderEventA);
		EventRouter.Subscribe("B", SenderEvent.Test, OnSenderEventB);
	}
	
	void OnSenderEventA(EventRouter.Event evt) {
		Console.WriteLine("Received A event);
	}

	void OnSenderEventB(EventRouter.Event evt) {
		Console.WriteLine("Received B event);
	}
}
```