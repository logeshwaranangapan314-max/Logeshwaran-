const express = require('express');
const app = express();

app.use(express.json());

let leaves = [];
let id = 1;

// Leave Apply API
app.post('/leave/apply', (req, res) => {
  const { employeeId, fromDate, toDate, reason } = req.body;
  const newLeave = { id: id++, employeeId, fromDate, toDate, reason, status: 'Pending' };
  leaves.push(newLeave);
  res.json({ message: 'Leave Applied Successfully', data: newLeave });
});

// Get All Leaves API
app.get('/leave/all', (req, res) => {
  res.json(leaves);
});

// Approve Leave API
app.put('/leave/:id/approve', (req, res) => {
  const leaveId = parseInt(req.params.id);
  const leave = leaves.find(l => l.id === leaveId);
  if (leave) {
    leave.status = 'Approved';
    res.json({ message: 'Leave Approved', data: leave });
  } else {
    res.status(404).json({ message: 'Leave Not Found' });
  }
});

// Reject Leave API
app.put('/leave/:id/reject', (req, res) => {
  const leaveId = parseInt(req.params.id);
  const leave = leaves.find(l => l.id === leaveId);
  if (!leave) {
    return res.status(404).json({ message: "Leave Not Found" });
  }
  leave.status = "Rejected";
  res.json(leave);
});

// Browser               
app.get('/', (req, res) => {
  res.send('<h1>HR Leave Tool API 🔥</h1><p>Server Running Successfully</p>');
});

app.listen(3000, () => console.log("Server running on port 3000"));