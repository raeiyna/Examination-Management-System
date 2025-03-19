# Examination-Management-System

from PySide6.QtWidgets import QApplication, QMainWindow, QStackedWidget, QPushButton, QWidget
from PySide6.QtUiTools import QUiLoader
import sys


class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()

        loader = QUiLoader()
        self.login_ui = loader.load(r"UI/login.ui", self)
        self.register_ui = loader.load(r"UI/register.ui", self)

        self.stacked_widget = QStackedWidget()
        self.stacked_widget.addWidget(self.login_ui)    
        self.stacked_widget.addWidget(self.register_ui)  

        self.setCentralWidget(self.stacked_widget)

        self.setup_connections()

    def setup_connections(self):
        login_btn = self.login_ui.findChild(QPushButton, "registeraccount")  
        register_btn = self.register_ui.findChild(QPushButton, "loginaccount")  

        if login_btn:
            login_btn.clicked.connect(self.show_register)

        if register_btn:
            register_btn.clicked.connect(self.show_login)

    def show_register(self):
        self.stacked_widget.setCurrentIndex(1)

    def show_login(self):
        self.stacked_widget.setCurrentIndex(0)


if __name__ == "__main__":
    app = QApplication(sys.argv)
    window = MainWindow()
    window.setWindowTitle("Examination Management System")
    window.resize(800, 600)  
    window.show()
    sys.exit(app.exec())
