# Pantheon Congestion Control Evaluation

This project is part of a networking assignment to evaluate and compare congestion control algorithms using [Pantheon](https://github.com/StanfordSNR/pantheon), a framework developed by Stanford for testing and analyzing transport protocols.

## Contents

- Pantheon experiment setup  
- Comparison of TCP congestion control algorithms: `cubic`, `bbr`, and `vegas`  
- Tests run under different network conditions  
- Results with throughput and delay graphs  
- PDF reports and performance summaries

##  Experiments

### 1. Test Scenario: 12Mbps, 50ms RTT
- Trace: `12mbps.trace`
- Duration: 30 seconds
- Algorithms tested: `cubic`, `bbr`, `vegas`
- Output stored in: `results_cubic_bbr/`

### 2. Test Scenario (Optional): 1Mbps, 200ms RTT
- Trace: `1mbps.trace` (created using `make_trace.py`)
- Duration: 30 seconds
- Output stored in: `results_1mbps_200ms/`

##  Results

Each test produces:
- `*.png`: Delay and throughput graphs
- `pantheon_summary.pdf`: Visual comparison of performance
- `pantheon_report.pdf`: Full LaTeX report including system config and metadata

## ⚙️ Setup

### Dependencies
- Ubuntu 20.04+ or 22.04
- Python 2.7
- pip packages: `matplotlib`, `numpy`, `pyyaml`
- Tools: `mahimahi`, `iperf`, `pdflatex`

### Installation (Summary)

sudo apt update
sudo apt install mahimahi iperf texlive-latex-recommended texlive-latex-extra
sudo pip2 install matplotlib numpy pyyaml


### Enable BBR (optional)

echo 'net.core.default_qdisc = fq' | sudo tee -a /etc/sysctl.conf
echo 'net.ipv4.tcp_congestion_control = bbr' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p

### Running a Test

python2.7 src/experiments/test.py local --schemes "cubic bbr vegas" --data-dir results_cubic_bbr
python2.7 src/analysis/analyze.py --data-dir results_cubic_bbr

To generate the LaTeX report:

python2.7 src/analysis/report.py --data-dir results_cubic_bbr

Output Structure

results_cubic_bbr/
├── cubic_datalink_throughput_run1.png
├── bbr_datalink_throughput_run1.png
├── cubic_datalink_delay_run1.png
├── bbr_datalink_delay_run1.png
├── pantheon_summary.pdf
├── pantheon_report.pdf
