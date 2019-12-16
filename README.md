# Let's Fly a Drone with JS

## Wes Bos Videos

Part 1 → <https://www.youtube.com/watch?v=JzFvGf7Ywkk>

Part 2 → <https://www.youtube.com/watch?v=ozMwRq-IT2w>

## Getting things started

### Frontend

1. `cd frontend`
1. `npm install`
1. `npm run dev`


### Backend
1. `cd backend`
1. `npm install`
1. connect to drone via wifi
1. `npm start`

## Getting Data From Backend

Get the socket from the socket.js.

```javascript
import socket from './socket';
```

Create two custom hooks 

```javascript
const useDroneState = () => {
  const [droneState, setDroneState] = useState({});
  useEffect(() => {
    socket.on('dronestate', setDroneState);
    return () => socket.removeListener('dronestate');
  }, []);
  return droneState;
}

const useSocket = () => {
  const [status, setStatus] = useState('DISCONNECTED');
  useEffect(() => {
    socket.on('status', setStatus);
    return () => socket.removeListener('status');
  }, []);
  return status;
}
```

```javascript
const status = useSocket();
const droneState = useDroneState([]);
```

## Sending Commands

```javascript
const sendCommand = command => {
  return function() {
    console.log(`Sending the command ${command}`);
    socket.emit('command', command);
  };
}
```
