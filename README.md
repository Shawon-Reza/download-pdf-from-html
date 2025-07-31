# download-pdf-from-html
npm install jspdf html2canvas


```jsx

import jsPDF from 'jspdf';
import html2canvas from 'html2canvas';

const DownloadPdf = () => {
  const downloadPDF = () => {
    const input = document.getElementById('pdf-content');
    html2canvas(input).then((canvas) => {
      const imgData = canvas.toDataURL('image/png');
      const pdf = new jsPDF();

      // Get page size (A4 by default)
      const pageWidth = pdf.internal.pageSize.getWidth();
      const pageHeight = pdf.internal.pageSize.getHeight();

      // Scale the image to fit within the A4 page
      const imgWidth = canvas.width;
      const imgHeight = canvas.height;

      const ratio = Math.min(pageWidth / imgWidth, pageHeight / imgHeight);
      const newWidth = imgWidth * ratio;
      const newHeight = imgHeight * ratio;

      // Add the image to the PDF
      pdf.addImage(imgData, 'PNG', 10, 10, newWidth, newHeight);

      // Save the PDF
      pdf.save('download.pdf');
    });
  };

  return (
    <div>
      <div id="pdf-content" style={{ padding: 20, background: '#fff' }}>
        <h2>My Report</h2>
        <p>This content will be converted to a PDF file.</p>
      </div>
      <button onClick={downloadPDF}>Download PDF</button>
    </div>
  );
};

export default DownloadPdf;



